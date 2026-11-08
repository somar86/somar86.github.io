---
title: "3D Inversion of Ultra-Deep Resistivity Measurements"
excerpt: "Inventor and developer of the industry's first 3D inversion of ultra-deep azimuthal resistivity (UDAR) measurements, mapping resistivity in 3D up to 300 ft away from the tool."
order: 1
toc: true
tags: [inversion, electromagnetics, geosteering, AI]
---

**Role:** Inventor and lead developer · **Organization:** Schlumberger-Doll Research / SLB

## Overview

I invented and developed the industry's **first 3D inversion of ultra-deep resistivity measurements**. It recovers the **resistivity distribution in 3D space up to 300 ft away from the tool**, turning ultra-deep azimuthal resistivity (UDAR) logging-while-drilling data into a volumetric image of the reservoir around the wellbore.

## The problem

UDAR tools are sensitive to formation boundaries and fluid contacts far from the wellbore, but conventional 1D and 2D inversions assume a layered or laterally invariant earth. Real reservoirs have faults, pinch-outs, channels, and lateral heterogeneity, so those assumptions break down exactly where geosteering decisions matter most.

## Approach

- **Voxel-based inversion:** the subsurface around the trajectory is discretized into voxels, and resistivity is estimated in each voxel with no prior assumption of layered geometry.
- **Physics-driven optimization:** a 3D electromagnetic forward model combined with regularized, gradient-based optimization reconciles the multi-frequency, multi-spacing UDAR measurements.
- **Real-time readiness:** the workflow is engineered for computational efficiency so it can run during drilling. Ongoing work uses **Transformers and diffusion models** to accelerate it further.

## Impact

- High-resolution **3D reservoir mapping and geosteering**, giving drillers and geoscientists a picture of structure and fluids in all directions around the well
- Part of the ultra-deep resistivity imaging portfolio deployed on SLB's digital platform

## Related work

- S. Omar, D. Salim, M. Zaslavsky, and L. Liang, "High-Resolution 3D Reservoir Mapping and Geosteering Using Voxel-Based Inversion Processing of UDAR Measurements," *SPWLA 65th Annual Symposium*, 2024.
- See also: [Look-ahead inversion](/projects/udar-look-ahead-inversion/)
