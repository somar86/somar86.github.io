---
# To publish: move to _posts/YYYY-MM-DD-ai-for-physics-part-2-fast-simulators.md (keep the name; later parts link to this URL).
title: "AI for Physics-Based Problems, Part 2: Fast Simulators and Learned Inverses"
excerpt: "Every AI-for-physics project starts with a forward simulator. Part 2 of the series covers why simulator speed and fidelity are the foundation of the pipeline, and how a learned inverse, quantized to run on an 8-bit edge processor, delivered a more than 17× speedup over physics-based inversion."
tags: [AI, physics-informed ML, inversion, edge AI, electromagnetics]
series: ai-for-physics
part: 2
mathjax: true
header:
  teaser: /assets/images/projects/npu-int8-inversion/icad2025-fig01-multitask-learning-architecture.jpg
---

In [Part 1](/blogs/ai-for-physics-based-problems/), I described what makes physics problems different from typical machine-learning tasks: labels are scarce, the problems are ill-posed, users need trust, and deployment is constrained. The classical answer is regularized inversion, which is rigorous but slow, because every iteration calls the forward model $$F$$. This part covers the first two patterns, which attack that speed bottleneck: making the simulator fast enough to teach a network, and then letting the network replace the inversion at run time.

{% include series-nav.html %}

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

---

A learned inverse is fast, but it is only as good as the data it learned from, and on its own it gives no sign when it is wrong. In Part 3, I take on both problems: how to combine laboratory, simulated, and field data without losing what each one teaches, and how to keep the physics in the loop as a referee for the network's answers.

{% include series-nav.html next=true %}
