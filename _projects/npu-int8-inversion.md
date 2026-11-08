---
title: "Real-Time Physics Inversion on 8-bit Integer NPUs"
excerpt: "First-ever deployment of regression-based physics inversion on 8-bit integer neural processing units, with near floating-point accuracy and a 17× speedup over the production inversion."
order: 4
toc: true
tags: [AI, edge computing, quantization, inversion]
header:
  teaser: /assets/images/projects/npu-int8-inversion/icad2025-fig01-multitask-learning-architecture.jpg
---

**Role:** Project lead and co-author · **Organization:** SLB

## Overview

Physics-based inversions are accurate but often too slow to run in real time on downhole or edge hardware. We trained a **multitask deep neural network** that predicts geophysical properties (formation density, photoelectric factor, and mud properties) and deployed it on a **Neural Processing Unit (NPU) using 8-bit integer arithmetic**. This was the first time such a regression-based physics inversion ran on INT8 hardware.

## The problem

Quantizing neural networks to low precision makes them fast and power-efficient, but it usually costs accuracy. That trade-off is acceptable for classification, but not for **continuous-valued regression**, where the outputs feed directly into petrophysical decisions.

## Approach

- **Multitask learning (MTL)** network trained to replace a production physics-based inversion
- **Per-layer quantization-aware training (QAT)** so the network learns to tolerate INT8 arithmetic
- **Noise-augmented synthetic training data** for robustness to real measurement noise
- Deployment and benchmarking on an embedded NPU

## Results

{% include figure popup=true image_path="/assets/images/projects/npu-int8-inversion/icad2025-fig01-multitask-learning-architecture.jpg" alt="Multitask learning network architecture" caption="Multitask learning network: a shared layer encodes the gamma-ray input, and task-specific branches predict formation and mud properties. *Chrifi, Omar & Hizem, IEEE ICAD 2025, Fig. 1.*" %}

{% include figure popup=true image_path="/assets/images/projects/npu-int8-inversion/icad2025-table03-fp32-vs-int8-quantization-accuracy.jpg" alt="Accuracy of FP32 vs INT8 quantization methods" caption="Accuracy of FP32 against standard INT8 post-training quantization, quantization-aware training, mixed precision, and the proposed per-layer QAT, which recovers near-FP32 accuracy on all outputs. *Chrifi, Omar & Hizem, IEEE ICAD 2025, Table III.*" %}

{% include figure popup=true image_path="/assets/images/projects/npu-int8-inversion/icad2025-table05-npu-latency-speedup.jpg" alt="Inference latency on CPU vs NPU" caption="Inference latency per sample on CPU (FP32), CPU (INT8), and the NPU, showing a 17× speedup over the existing inversion. *Chrifi, Omar & Hizem, IEEE ICAD 2025, Table V.*" %}

## Impact

- **Near floating-point accuracy** at 8-bit integer precision
- **Over 17× speedup** compared with the production inversion algorithm, which is accurate but cannot run in real time
- Opens the door to in-situ, real-time decision-making on next-generation edge computing hardware

## Related work

- O. Chrifi, S. Omar, and M. Hizem, "[High accuracy preserving regression-based physics inversion workflow deployment on 8-bit integer computing hardware](https://doi.org/10.1109/ICAD65464.2025.11114064)," *IEEE ICAD*, 2025.
