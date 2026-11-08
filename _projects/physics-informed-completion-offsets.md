---
title: "Physics-Informed Deep Learning for Cased-Hole Spectroscopy"
excerpt: "A deep learning pipeline with mixed-data transfer learning that automates completion-offset corrections in neutron-induced gamma-ray spectroscopy, replacing a manual, expert-driven iterative workflow."
order: 5
toc: true
tags: [AI, deep learning, transfer learning, petrophysics]
header:
  teaser: /assets/images/projects/physics-informed-completion-offsets/icad2025-fig08-capture-offset-predictions-residuals.jpg
---

**Role:** Project lead, co-author, and co-inventor · **Organization:** SLB

## Overview

In cased wells, neutron-induced gamma-ray spectroscopy measures the elemental composition of the formation. The signal also contains contributions from the steel casing and the cement, which must be removed as **completion offsets** before the formation-specific elemental yields can be interpreted. We developed a **physics-informed deep learning pipeline** that predicts these offsets automatically.

## The problem

Finding completion offsets has been a manual, iterative exercise led by subject-matter experts, slow and hard to reproduce. Conventional transfer learning from laboratory data to field data fails because of **catastrophic forgetting**: a model fine-tuned on field data loses what it learned in the lab.

## Approach

- **Mixed-data transfer learning:** models are trained on combined laboratory and field data from the outset, rather than pretraining on one and fine-tuning on the other.
- **Physics-informed features:** spectral yields, formation properties, geometric parameters such as cement and casing areas, and engineered feature combinations.
- **Domain-knowledge data augmentation:** using the cement-fraction method, calcium contributions from cement were added to the laboratory data, extending the model to carbonate formations.

## Results

{% include figure popup=true image_path="/assets/images/projects/physics-informed-completion-offsets/icad2025-fig08-capture-offset-predictions-residuals.jpg" alt="Predicted vs true capture offsets with residuals" caption="Predicted versus true capture offsets for iron, silicon, and calcium (near and far detectors), with residuals, for models trained on combined laboratory/synthetic data (blue) and field data (red). *Benrabh, Miles, Omar & Mosse, IEEE ICAD 2025, Fig. 8.*" %}

## Impact

- Consistently meets the target accuracies: **0.01** for cement capture offsets (silicon and calcium), **0.03** for casing capture offset (iron), and a normalized value of **10** for the inelastic calcium offset
- Replaces a manual, expert-driven workflow with an automated, reproducible one
- The calibration and data-mixing transfer-learning methods are the subject of a patent application

## Related work

- W. Benrabh, J. Miles, S. Omar, and L. Mosse, "[Physics-informed deep learning prediction of completion offsets for automated cased-hole petrophysical analysis](https://doi.org/10.1109/ICAD65464.2025.11114056)," *IEEE ICAD*, 2025.
- S. Omar, L. Mosse, J. Miles, and W. Benrabh, "[Physics-enforced deep learning calibration and data-mixing transfer learning methods](https://patents.google.com/patent/WO2026169983A1/en)," WO 2026/169983 A1, 2026.
