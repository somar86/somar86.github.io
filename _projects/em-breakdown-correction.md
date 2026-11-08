---
title: "Single-Shot Correction for Low/High-Frequency EM Breakdown"
excerpt: "An electromagnetics formulation that removes the need to stitch together separate low- and high-frequency solvers by correcting the root cause of numerical breakdown in a single shot."
order: 6
toc: true
tags: [computational electromagnetics, numerical methods]
---

**Role:** Co-developer (PhD research) · **Organization:** Purdue University

## Overview

I helped develop an electromagnetics formulation that **removes the need to stitch together multiple solvers** for low- and high-frequency applications. Instead of switching models across the spectrum, it applies a **single-shot correction to the root cause of the numerical breakdown** in the simulation.

## The problem

The electric field integral equation (EFIE) is a workhorse of full-wave simulation, but it **breaks down at low frequencies**: the system becomes severely ill-conditioned and the solution loses accuracy. The usual workaround is to combine separate low-frequency (quasi-static) and high-frequency (full-wave) solvers and stitch their results together. That adds complexity and can introduce errors at the transition.

## Approach

- Identified the **root mathematical cause** of the breakdown, rather than treating symptoms with special basis functions or preconditioners
- Derived a **single-shot correction** applied to the solution obtained from the original EFIE, recovering an accurate solution in one step
- Works across the frequency spectrum with **one formulation**

## Impact

- One solver for both low- and high-frequency analysis, with no solver stitching
- Simpler, more robust broadband simulation workflows for circuits and scattering problems

## Related work

- J. Zhu, S. Omar, and D. Jiao, "Solution to the electric field integral equation when it breaks down," *IEEE Trans. Antennas and Propagation*, vol. 62, no. 8, pp. 4122–4134, Aug. 2014.
