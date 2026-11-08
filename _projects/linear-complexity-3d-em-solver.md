---
title: "Linear-Complexity Full-Wave 3D EM Solver for Circuits"
excerpt: "Inventor and developer of the semiconductor industry's first linear time complexity full 3D electromagnetics solver for circuit analysis at arbitrary frequency."
order: 4
toc: true
tags: [computational electromagnetics, fast solvers, semiconductors, HPC]
---

**Role:** Inventor and developer (PhD research) · **Organization:** Purdue University · **Funding:** NSF and Department of Defense

## Overview

I invented and developed the semiconductor industry's **first linear time complexity, full 3D electromagnetics solver** for circuit analysis at **arbitrary electromagnetic frequency**. Solve time and memory grow only linearly, O(N), with the number of unknowns, which makes full-wave analysis practical for large, realistic integrated circuits.

## The problem

Full-wave integral-equation methods are accurate but lead to dense system matrices. Direct solution costs O(N³) time and O(N²) memory, which quickly becomes prohibitive for chip-scale problems with complex, inhomogeneous materials. Designers often fall back on approximate quasi-static models that lose accuracy at high frequencies.

## Approach

- **Volume integral equation (VIE)** formulation that handles inhomogeneous dielectrics and conductors in 3D
- **Hierarchical matrix (quad-tree based) compression** exploiting the low-rank structure of far-field interactions, implemented in C/C++
- **Direct solver with linear complexity:** a fast direct factorization and inversion, avoiding the convergence problems of iterative solvers on ill-conditioned circuit problems
- Also delivered O(N) iterative and O(N log N) direct inverse VIE solvers for electromagnetic scattering problems

## Impact

- Real-time O(N) solutions for circuit design problems
- Full-wave accuracy at any frequency without switching between low- and high-frequency models

## Related work

- S. Omar and D. Jiao, "A linear complexity direct volume integral equation solver for full-wave 3-D circuit extraction in inhomogeneous materials," *IEEE Trans. Microwave Theory and Techniques*, vol. 63, no. 3, pp. 897–912, 2015. [doi:10.1109/TMTT.2015.2396494](https://doi.org/10.1109/TMTT.2015.2396494)
- See also: [Radiation-aware 3D VIE formulation](/projects/vie-radiation-hardened-chips/) and [Single-shot low/high-frequency breakdown correction](/projects/em-breakdown-correction/)
