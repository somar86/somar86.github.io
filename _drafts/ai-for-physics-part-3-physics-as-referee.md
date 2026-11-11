---
# To publish: move to _posts/YYYY-MM-DD-ai-for-physics-part-3-physics-as-referee.md (keep the name; later parts link to this URL).
title: "AI for Physics-Based Problems, Part 3: Real-World Data and Physics as Referee"
excerpt: "Speed alone does not make a tool engineers trust. Part 3 of the series covers why training on mixed lab, simulated, and field data beat transfer learning, and how the forward model, covariance, and misfit turn a network's prediction into a verifiable one."
tags: [AI, physics-informed ML, inversion, edge AI, electromagnetics]
series: ai-for-physics
part: 3
mathjax: true
header:
  teaser: /assets/images/projects/multi-casing-corrosion/aip2017-fig12-field-log-three-casing-inversion.jpg
---

[Part 2](/blogs/ai-for-physics-part-2-fast-simulators/) showed how to buy speed: a fast simulator generates perfectly labeled training data, and a network trained on it replaces a slow inversion at run time, fast enough to run on an 8-bit edge processor. But speed alone does not make a tool engineers use. Two of the challenges from [Part 1](/blogs/ai-for-physics-based-problems/) are still open: field data comes without labels, and users need to trust the answer. This part covers the two patterns that address them.

{% include series-nav.html %}

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

---

So far in this series, AI has served as a fast approximation of physics we already know how to compute, with the forward model keeping it honest. In Part 4, AI takes on two different roles: helping to discover new physics in the form of closed-form equations, and generating many plausible answers for problems that have more than one.

{% include series-nav.html next=true %}
