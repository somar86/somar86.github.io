---
# To publish: move to _posts/YYYY-MM-DD-ai-for-physics-part-4-generative-models.md (keep the name; later parts link to this URL).
title: "AI for Physics-Based Problems, Part 4: Discovering Physics and Generative Models"
excerpt: "AI can do more than approximate known physics. Part 4 of the series covers using data to find closed-form models for real-time decisions, and why transformers and diffusion models suit non-unique 3D inverse problems."
tags: [AI, physics-informed ML, inversion, edge AI, electromagnetics]
series: ai-for-physics
part: 4
header:
  teaser: /assets/images/projects/udar-3d-inversion/fig04-3d-voxel-inversion-l-shaped-model.jpg
---

In [Part 2](/blogs/ai-for-physics-part-2-fast-simulators/) and [Part 3](/blogs/ai-for-physics-part-3-physics-as-referee/), AI played one main role: a fast approximation of physics we already know how to compute, trained on simulations and kept honest by the forward model. The last two patterns go further. The first uses data to *find* physics, in the form of equations engineers can trust. The second takes on the ill-posedness from [Part 1](/blogs/ai-for-physics-based-problems/) directly, with models that return a distribution of plausible answers instead of a single one.

{% include series-nav.html %}

## Pattern 5: Use AI to discover physics, not only to approximate it

AI is usually framed as a replacement for analytical models, but it can also help find them. In work on hydraulic stimulation, we derived **closed-form analytical models that predict the entry points of stimulation fluid from water-hammer signals**, the pressure waves that travel up and down a well after a sudden change in pumping. We also developed predictive models for the reflection time of tube waves in low-frequency water-hammer data.

Closed-form models have advantages that no neural network can match. They are transparent, they extrapolate in physically sensible ways, and they run instantly on any hardware. That enables **real-time corrective actions** during a stimulation job. In this mode of work, data-driven analysis is a guide that points to the right functional relationships, and physics reasoning turns them into equations engineers can trust.

## Pattern 6: Generative models for problems with many answers

Deep-reading electromagnetic measurements such as ultra-deep azimuthal resistivity (UDAR) are sensitive to the formation in three dimensions, far beyond the wellbore. Our [voxel-based 3D inversion](/projects/udar-3d-inversion/) recovers this full 3D picture. It uses a nonuniform voxel grid, an exact 3D electromagnetic simulator in the loop, and an adaptively regularized Gauss–Newton optimizer.

{% include figure popup=true image_path="/assets/images/projects/udar-3d-inversion/fig06-true-vs-inverted-sand-injectites.jpg" alt="True vs inverted 3D model of sand injectites" caption="True 3D model of sand-injectite 'fingers' above a main sand body (left) and the voxel-inversion reconstruction (right). *Omar et al., SPWLA 2024.*" %}

Full 3D inversion is computationally demanding, and the problem is fundamentally non-unique: several 3D models can explain the same data. This is exactly where newer architectures become interesting. **Transformers** can capture long-range relationships along a well trajectory, and **diffusion models** learn a *distribution* of plausible models rather than a single answer. That matches the non-unique nature of the inverse problem, and it opens a path to uncertainty quantification. I am currently exploring both for real-time processing of 3D UDAR inversions. The guiding principle is the same one from Part 3: the generative model proposes, and the physics verifies.

---

That completes the six patterns. In the final part, I turn them into a practical checklist of the questions I work through when starting a new AI-for-physics project.

{% include series-nav.html next=true %}
