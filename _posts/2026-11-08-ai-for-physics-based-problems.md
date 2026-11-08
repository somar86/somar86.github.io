---
title: "AI for Physics-Based Problems: Lessons from Inversion, Imaging, and Edge Deployment"
excerpt: "Physics problems are not typical machine-learning problems. Six patterns from more than a decade of work in subsurface imaging, well integrity, and computational electromagnetics on where AI helps, where physics must stay in charge, and how to combine the two."
tags: [AI, physics-informed ML, inversion, edge AI, electromagnetics]
toc: true
toc_sticky: true
mathjax: true
header:
  teaser: /assets/images/projects/udar-3d-inversion/fig06-true-vs-inverted-sand-injectites.jpg
---

Most of my career has been spent solving **inverse problems**: inferring what we cannot see (rock properties hundreds of feet from a well, the thickness of a corroded casing behind three other pipes, the currents flowing in a chip) from measurements we can make. These problems are governed by well-understood physics, usually Maxwell's equations, and for decades the standard way to solve them has been physics-based inversion: simulate, compare with data, update, repeat.

Over the last few years, AI has changed how I approach these problems. It has not replaced the physics. Instead, it has changed **where the physics lives** in the workflow. This article distills the patterns that have worked in practice, with examples from my own projects.

## Why physics problems are different

It is tempting to treat a physics problem like any other supervised-learning task: collect inputs and outputs, train a network, deploy. That rarely works, for four reasons:

1. **Labels are scarce or nonexistent.** There is no ground truth for the resistivity 200 ft away from a well or the true wall thickness of a buried casing. Field data comes without answers.
2. **The problems are ill-posed.** Many different earth models explain the same measurements equally well. A network trained to output a single answer will happily give a confident wrong one.
3. **Users need trust, not just accuracy.** A geosteering or well-integrity decision can cost millions. Engineers need to know *why* an answer is right and *how uncertain* it is.
4. **Deployment is constrained.** The most valuable answers are needed in real time, downhole or at the wellsite, on hardware with tight power and compute budgets.

The classical tool for these problems is regularized inversion. Given measurements $$\mathbf{d}$$ and a forward model $$F$$ that simulates the measurement for a model $$\mathbf{m}$$ of the subsurface, we solve:

$$
\mathbf{m}^\star = \arg\min_{\mathbf{m}} \; \left\lVert \mathbf{W}_d \left[ \mathbf{d} - F(\mathbf{m}) \right] \right\rVert^2 + \lambda \left\lVert \mathbf{W}_m \mathbf{m} \right\rVert^2
$$

The first term asks the model to explain the data. The second, the regularization, encodes prior knowledge and tames the ill-posedness. This framework is rigorous, interpretable, and gives uncertainty estimates, but it can be slow, because every iteration requires forward simulations and sensitivities. Every pattern below is, in some way, about keeping the rigor of this equation while removing its bottlenecks.

## Pattern 1: Make the simulator fast, then let it teach

Every AI-for-physics project I have worked on starts with a forward simulator, because the simulator is the only source of perfectly labeled data. For any model $$\mathbf{m}_i$$ we choose, it gives the exact measurement $$F(\mathbf{m}_i)$$. That makes **simulator speed and fidelity the foundation of the whole pipeline**.

This is why my early work on fast solvers still matters to my AI work today. During my PhD, I developed [linear-complexity electromagnetic solvers](/projects/linear-complexity-3d-em-solver/) whose time and memory grow only as O(N) with problem size, inverting dense systems with over two million unknowns in under an hour on a single CPU core. Today the same idea, fast exact physics, is what makes it feasible to generate the large volumes of training examples that a network needs.

Two lessons stand out:

- **Sample the model space deliberately.** A network only learns what the training models contain. If your synthetic earth never contains a thin resistive layer next to a fault, the network will not recognize one.
- **Simulate the measurement, not just the physics.** Real tools have calibration errors, drift, and noise. In our [NPU inversion work](/projects/npu-int8-inversion/), we modeled each observed signal as

$$
\mathbf{x}_{\text{obs}} = \mathbf{x} + \boldsymbol{\epsilon}_{\text{sys}} + \boldsymbol{\epsilon}_{\text{stat}} + \boldsymbol{\epsilon}_{\text{rand}},
$$

with systematic, statistical, and random noise injected into the synthetic data. Training on clean simulations and testing on noisy field data is one of the most common reasons physics-trained networks fail in the field.

## Pattern 2: Learn the inverse when speed is the bottleneck

Once a simulator can generate data, we can train a network $$G_\theta$$ to approximate the inverse map directly, from measurements to properties:

$$
\theta^\star = \arg\min_{\theta} \sum_i \left\lVert G_\theta\!\left( F(\mathbf{m}_i) + \boldsymbol{\epsilon}_i \right) - \mathbf{m}_i \right\rVert^2
$$

The expensive physics is paid for once, during training. At run time, inference is a single forward pass of the network.

We took this idea to its practical limit by deploying a regression-based physics inversion on an **8-bit integer neural processing unit (NPU)**, the kind of low-power accelerator found in embedded and edge devices. A multitask network predicts formation properties (density, photoelectric factor) and mud properties at the same time, sharing a common encoder of the gamma-ray input.

{% include figure popup=true image_path="/assets/images/projects/npu-int8-inversion/icad2025-fig01-multitask-learning-architecture.jpg" alt="Multitask learning network architecture" caption="Multitask network for real-time physics inversion: a shared layer encodes the measurements, and task-specific branches predict formation and mud properties. *Chrifi, Omar & Hizem, IEEE ICAD 2025.*" %}

The hard part was not training the network but **quantizing it**. Quantization to 8-bit integers works well for classification, where small numerical errors rarely change the predicted class. Regression is far less forgiving: rounding errors flow straight into the predicted physical property. Our solution was a **per-layer quantization-aware training** scheme that keeps higher precision in the first and last layers, where rounding hurts continuous outputs most, and quantizes the intermediate layers to 8 bits. The result was near floating-point accuracy and a **more than 17× speedup** over the production physics-based inversion, which is accurate but cannot run in real time.

**When to use this pattern:** when the physics-based inversion is trusted but too slow for the decision it supports, and when the measurement configuration is fixed enough that a single trained network covers the use cases.

## Pattern 3: Blend lab, simulation, and field data from the start

Physics problems usually come with data from very different worlds: controlled laboratory experiments with known answers, simulations, and field measurements that reflect reality but lack labels. The obvious approach is **transfer learning**: train on the lab data, then fine-tune on field data.

In our work on [cased-hole spectroscopy](/projects/physics-informed-completion-offsets/), that obvious approach failed. When we fine-tuned a lab-trained model on field data, it suffered **catastrophic forgetting**, losing what it had learned from the controlled experiments. What worked was training on a **mixed dataset from the outset**, combining laboratory, simulated, and field data, with physics-informed input features such as spectral yields, formation properties, and the cement and casing areas.

We also used physics to *create* data the lab could not provide. Using a first-principles cement-fraction method, we systematically added the calcium contribution of cement to laboratory samples, which extended the model to carbonate formations. The resulting models met the target accuracies (0.01 for the cement capture offsets and 0.03 for the casing iron offset) and replaced a manual, expert-driven iterative workflow.

{% include figure popup=true image_path="/assets/images/projects/physics-informed-completion-offsets/icad2025-fig08-capture-offset-predictions-residuals.jpg" alt="Predicted vs true capture offsets" caption="Predicted versus true completion offsets, with residuals, for models trained on combined laboratory/synthetic data (blue) and field data (red). *Benrabh, Miles, Omar & Mosse, IEEE ICAD 2025.*" %}

**The lesson:** physics knowledge is most valuable in the data and features, not only in the model architecture. Augmenting data with first-principles corrections is often simpler and more robust than designing an exotic physics-constrained network.

## Pattern 4: Keep the physics in the loop as the referee

A network's prediction is a hypothesis. The forward model can test it. For any predicted model $$\hat{\mathbf{m}} = G_\theta(\mathbf{d})$$, we can compute the data residual

$$
r = \left\lVert \mathbf{d} - F\!\left( G_\theta(\mathbf{d}) \right) \right\rVert ,
$$

which tells us whether the prediction actually explains the measurements. This simple check is one of the most powerful ideas in AI for physics. It turns a black-box prediction into a verifiable one, and it flags inputs that fall outside the training distribution.

This is also where classical inversion keeps its edge. In my [multi-casing corrosion](/projects/multi-casing-corrosion/) work, the inversion delivers more than a thickness for each pipe:

- The inversion-derived **covariance matrix** provides uncertainty estimates for every inverted thickness.
- The **data resolution matrix** reveals the information content of each measurement channel, which guided channel weighting, frequency selection, and sensor design.
- The **inversion misfit** acts as a quality-control flag, for example to detect tool and casing eccentering.

{% include figure popup=true image_path="/assets/images/projects/multi-casing-corrosion/aip2017-fig12-field-log-three-casing-inversion.jpg" alt="Three-casing field log inversion with mismatch track" caption="Field log from a three-casing well: the inverted thickness of each casing, with the inversion mismatch used as a quality-control indicator. *Omar & Omeragic, AIP Conf. Proc. 1806, 2017.*" %}

The best hybrid systems use AI where it is strong (speed, pattern recognition, good starting models) and physics where it is strong (verification, uncertainty, extrapolation). A network that provides the starting model for a few Gauss–Newton iterations can offer the best of both: the inversion converges in a fraction of the time and still ends with a model that demonstrably fits the data.

## Pattern 5: Use AI to discover physics, not only to approximate it

AI is usually framed as a replacement for analytical models, but it can also help find them. In work on hydraulic stimulation, we derived **closed-form analytical models that predict the entry points of stimulation fluid from water-hammer signals**, the pressure waves that travel up and down a well after a sudden change in pumping. We also developed predictive models for the reflection time of tube waves in low-frequency water-hammer data.

Closed-form models have advantages that no neural network can match. They are transparent, they extrapolate in physically sensible ways, and they run instantly on any hardware. That enables **real-time corrective actions** during a stimulation job. In this mode of work, data-driven analysis is a guide that points to the right functional relationships, and physics reasoning turns them into equations engineers can trust.

## Pattern 6: Generative models for problems with many answers

Deep-reading electromagnetic measurements such as ultra-deep azimuthal resistivity (UDAR) are sensitive to the formation in three dimensions, far beyond the wellbore. Our [voxel-based 3D inversion](/projects/udar-3d-inversion/) recovers this full 3D picture. It uses a nonuniform voxel grid, an exact 3D electromagnetic simulator in the loop, and an adaptively regularized Gauss–Newton optimizer.

{% include figure popup=true image_path="/assets/images/projects/udar-3d-inversion/fig06-true-vs-inverted-sand-injectites.jpg" alt="True vs inverted 3D model of sand injectites" caption="True 3D model of sand-injectite 'fingers' above a main sand body (left) and the voxel-inversion reconstruction (right). *Omar et al., SPWLA 2024.*" %}

Full 3D inversion is computationally demanding, and the problem is fundamentally non-unique: several 3D models can explain the same data. This is exactly where newer architectures become interesting. **Transformers** can capture long-range relationships along a well trajectory, and **diffusion models** learn a *distribution* of plausible models rather than a single answer. That matches the non-unique nature of the inverse problem, and it opens a path to uncertainty quantification. I am currently exploring both for real-time processing of 3D UDAR inversions. The guiding principle stays the same: the generative model proposes, and the physics verifies.

## A practical checklist

When I start a new AI-for-physics project, I work through these questions:

1. **What exactly is the bottleneck?** Speed, missing labels, unknown physics, or deployment hardware? The answer determines which pattern applies.
2. **Is the simulator fast and faithful enough?** If not, fix that first. Everything downstream inherits its errors.
3. **Does the training data look like the field?** Model the measurement chain, noise, and calibration, not just ideal physics.
4. **How will a wrong answer be detected?** Plan for a physics residual check or a quality-control flag from day one.
5. **What uncertainty does the user need?** A single number is rarely enough for a high-stakes decision.
6. **Where will it run?** Edge and downhole hardware may require quantization, smaller architectures, and per-layer precision choices.
7. **Who needs to trust it?** Involve domain experts early. Their intuition is the best test set you have.

## Closing thoughts

The most successful projects I have been part of did not ask "can AI replace the physics?" They asked "**where should the physics live?**" Sometimes it lives in the simulator that generates the training data, sometimes in the features, sometimes in a residual check that referees the network, and sometimes in a closed-form equation that the data helped reveal. Treating AI and physics as partners rather than competitors is what turns a promising prototype into a tool that engineers use every day.

*If you are working on similar problems, I would be glad to connect on [LinkedIn](https://www.linkedin.com/in/saadomar/). For details of the work described here, see my [projects](/projects/) and [publications](/publications/).*
