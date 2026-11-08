---
title: "3D Inversion of Ultra-Deep Resistivity Measurements"
excerpt: "Inventor and developer of the industry's first 3D inversion of ultra-deep azimuthal resistivity (UDAR) measurements, mapping resistivity in 3D up to 300 ft away from the tool."
order: 1
toc: true
tags: [inversion, electromagnetics, geosteering, AI]
header:
  teaser: /assets/images/projects/udar-3d-inversion/fig06-true-vs-inverted-sand-injectites.jpg
---

**Role:** Inventor and lead developer · **Organization:** Schlumberger-Doll Research / SLB

## Overview

I invented and developed the industry's **first 3D inversion of ultra-deep resistivity measurements**. It recovers the **resistivity distribution in 3D space up to 300 ft away from the tool**, turning ultra-deep azimuthal resistivity (UDAR) logging-while-drilling data into a volumetric image of the reservoir around the wellbore.

## The problem

UDAR measurements have full 3D volumetric sensitivity to the surrounding formation, but routine processing relies on layered-earth (1D) models, refined on demand with 2D processing. Existing 3D processing on hierarchical Cartesian grids smooths the formation strongly and produces artifacts away from the wellbore, losing the resolution of 2D imaging. Real reservoirs have channels, injectites, faults, and lateral heterogeneity, so high-resolution, accurate 3D mapping is critical for precise geosteering and well placement.

## Approach

- **Voxel-based imaging:** a minimally biased inversion on a **nonuniform 3D voxel discretization** maps arbitrary 3D heterogeneities using the full 3D sensitivities of the measurements.
- **Exact 3D physics in the loop:** a full 3D electromagnetic simulator, handling arbitrary geometry and general anisotropy on a tool-centered staggered nonuniform Lebedev grid, reconstructs the tool response.
- **Adaptively regularized Gauss–Newton optimization** inverts the complete set of eight triaxial deep EM measurements at multiple frequencies and up to three transmitter–receiver spacings. Gradient-based regularization yields sharp, blocky resistivity images rather than smeared ones.
- **Validated on geologically realistic synthetic models** with known ground truth: sand injectites, shale channels, and residual-oil sands.
- Ongoing work applies **Transformers and diffusion models** for real-time processing of 3D inversions.

## Results

These results are from the SPWLA 2024 paper. Each case starts from a geologically realistic 3D model, and the voxel inversion images the formation in real time as the tool drills through it.

{% include figure popup=true image_path="/assets/images/projects/udar-3d-inversion/fig03-handbrake-turn-sand-injectite-model.jpg" alt="Outcrop of a sand injectite and the derived L-shaped 3D resistivity model" caption="An outcrop of a 'handbrake turn' sand injectite (Panoche Hills, California) and the L-shaped 3D resistivity model built from it, with the well trajectory. *Omar et al., SPWLA 2024, Fig. 3.*" %}

{% include figure popup=true image_path="/assets/images/projects/udar-3d-inversion/fig04-3d-voxel-inversion-l-shaped-model.jpg" alt="3D voxel inversion snapshots for the L-shaped model" caption="3D voxel inversion of the L-shaped model, updated every 3 m as the transmitter moves from −20 m to 16 m. The sideways branch of the formation is resolved around and ahead of the tool. *Omar et al., SPWLA 2024, Fig. 4.*" %}

{% include figure popup=true image_path="/assets/images/projects/udar-3d-inversion/fig06-true-vs-inverted-sand-injectites.jpg" alt="True vs inverted 3D model of sand injectites" caption="True 3D model of three sand-injectite 'fingers' above a main sand body (left) and the voxel-inversion reconstruction (right). The location, size, and spacing of the fingers are recovered. *Omar et al., SPWLA 2024, Fig. 6.*" %}

{% include figure popup=true image_path="/assets/images/projects/udar-3d-inversion/fig07-sand-injectite-inversion-sequence.jpg" alt="Real-time sequence of sand-injectite 3D inversions" caption="The sand-injectite inversion updating in real time as the tool moves from −28 m to 32 m, with a top view of the final result next to the true model. *Omar et al., SPWLA 2024, Fig. 7.*" %}

{% include figure popup=true image_path="/assets/images/projects/udar-3d-inversion/fig09-shale-avoidance-inversion.jpg" alt="3D imaging of thin shale channels for shale avoidance" caption="Shale avoidance: imaging two thin, asymmetrically placed shale channels inside a resistive sand as the tool moves from −6 m to 21 m. *Omar et al., SPWLA 2024, Fig. 9.*" %}

{% include figure popup=true image_path="/assets/images/projects/udar-3d-inversion/fig11-residual-oil-inversion.jpg" alt="3D imaging of resistive oil-bearing sand channels in shale" caption="Residual oil: imaging two resistive, oil-bearing sand channels inside a conductive shale as the tool moves from 3 m to 39 m. *Omar et al., SPWLA 2024, Fig. 11.*" %}

## Impact

- High-resolution **3D reservoir mapping and geosteering**, giving drillers and geoscientists a picture of structure and fluids in all directions around the well
- Part of the ultra-deep resistivity imaging portfolio deployed on SLB's digital platform

## Related work

- S. Omar, D. Salim, M. Zaslavsky, and L. Liang, "High-Resolution 3D Reservoir Mapping and Geosteering Using Voxel-Based Inversion Processing of UDAR Measurements," *SPWLA 65th Annual Symposium*, 2024.
- See also: [Look-ahead inversion](/projects/udar-look-ahead-inversion/)
