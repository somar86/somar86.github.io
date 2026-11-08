---
title: "Linear-Complexity Full-Wave 3D EM Solver for Circuits"
excerpt: "Inventor and developer of the semiconductor industry's first linear time complexity full 3D electromagnetics solver for circuit analysis at arbitrary frequency."
order: 8
toc: true
tags: [computational electromagnetics, fast solvers, semiconductors, HPC]
header:
  teaser: /assets/images/projects/linear-complexity-3d-em-solver/tmtt2015-fig05-on-chip-bus-array-linear-scaling.jpg
---

**Role:** Inventor and developer (PhD research) · **Organization:** Purdue University · **Funding:** NSF and Department of Defense

## Overview

I invented and developed the semiconductor industry's **first linear time complexity, full 3D electromagnetics solver** for circuit analysis at **arbitrary electromagnetic frequency**. Solve time and memory grow only linearly, O(N), with the number of unknowns, which makes full-wave analysis practical for large, realistic integrated circuits.

## The problem

Full-wave integral-equation methods are accurate but lead to dense system matrices. Direct solution costs O(N³) time and O(N²) memory, which quickly becomes prohibitive for chip-scale problems with complex, inhomogeneous materials. Designers often fall back on approximate quasi-static models that lose accuracy at high frequencies.

## Approach

- A **well-conditioned volume integral equation (VIE)** formulation for arbitrarily shaped lossy conductors in inhomogeneous dielectrics, with ports anywhere in the layout. It enables a robust direct solution even with a rank-1 representation.
- **Hierarchical matrix (quad-tree based) compression** exploiting the low-rank structure of far-field interactions, implemented in C/C++
- **Direct solver with linear complexity:** a fast direct factorization and inversion, avoiding the convergence problems of iterative solvers on ill-conditioned circuit problems
- Also delivered O(N) iterative and O(N log N) direct inverse VIE solvers for electromagnetic scattering problems

## Results

{% include figure popup=true image_path="/assets/images/projects/linear-complexity-3d-em-solver/tmtt2015-fig05-on-chip-bus-array-linear-scaling.jpg" alt="On-chip bus arrays and linear scaling of time and memory" caption="On-chip bus arrays from 4×4 to 64×64 conductors (about 1 million unknowns): (a) a 16×16 array, (b) matrix representation error, (c) inverse error, and (d) CPU time and memory, which grow **linearly** with the number of unknowns. *Omar & Jiao, IEEE TMTT 2015, Fig. 5.*" %}

{% include figure popup=true image_path="/assets/images/projects/linear-complexity-3d-em-solver/tmtt2015-fig07-spiral-inductor-array-linear-scaling.jpg" alt="Spiral inductor arrays and linear scaling" caption="Arrays of irregularly shaped on-chip spiral inductors from 2×2 to 64×64 (up to about 2 million unknowns), again showing linear time and memory and controlled error. *Omar & Jiao, IEEE TMTT 2015, Fig. 7.*" %}

{% include figure popup=true image_path="/assets/images/projects/linear-complexity-3d-em-solver/jmmct2017-fig13-dielectric-cube-array.jpg" alt="Large dielectric cube array" caption="Large dielectric-cube arrays, from 2×2×2 up to 14×14×14 cubes (about 1.04 million unknowns), used to benchmark the direct and iterative solvers for electrodynamic scattering. *Omar, Ma & Jiao, IEEE JMMCT 2017, Fig. 13.*" %}

{% include figure popup=true image_path="/assets/images/projects/linear-complexity-3d-em-solver/jmmct2017-fig06-multilayer-dielectric-sphere-rcs.jpg" alt="Multilayer dielectric sphere RCS vs Mie series" caption="Radar cross section of an eight-layer dielectric sphere: the proposed direct and iterative solvers both match the analytical Mie-series solution. *Omar, Ma & Jiao, IEEE JMMCT 2017, Fig. 6.*" %}

{% include figure popup=true image_path="/assets/images/projects/linear-complexity-3d-em-solver/iet2013-fig08-storage-and-time-vs-conventional.jpg" alt="Storage and solution time vs conventional solver" caption="Storage (a) and total solution time (b) of the 𝓗²-matrix volume integral solver compared with a conventional solver, showing near-linear growth versus the conventional solver's steep rise. *Omar & Jiao, IET MAP 2013, Fig. 8.*" %}

## Impact

- Inverts dense system matrices with **over 2 million unknowns in under 1 hour on a single 3 GHz CPU core**
- Real-time O(N) solutions for circuit design problems
- Full-wave accuracy at any frequency without switching between low- and high-frequency models

## Related work

- S. Omar and D. Jiao, "A linear complexity direct volume integral equation solver for full-wave 3-D circuit extraction in inhomogeneous materials," *IEEE Trans. Microwave Theory and Techniques*, vol. 63, no. 3, pp. 897–912, 2015. [doi:10.1109/TMTT.2015.2396494](https://doi.org/10.1109/TMTT.2015.2396494)
- See also: [Radiation-aware 3D VIE formulation](/projects/vie-radiation-hardened-chips/) and [Single-shot low/high-frequency breakdown correction](/projects/em-breakdown-correction/)
