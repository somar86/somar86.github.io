---
title: "Single-Shot Correction for Low/High-Frequency EM Breakdown"
excerpt: "An electromagnetics formulation that removes the need to stitch together separate low- and high-frequency solvers by correcting the root cause of numerical breakdown in a single shot."
order: 10
toc: true
tags: [computational electromagnetics, numerical methods]
header:
  teaser: /assets/images/projects/em-breakdown-correction/tap2014-fig04-sphere-rcs-1hz-and-1ghz.jpg
---

**Role:** Co-developer (PhD research) · **Organization:** Purdue University

## Overview

I helped develop an electromagnetics formulation that **removes the need to stitch together multiple solvers** for low- and high-frequency applications. Instead of switching models across the spectrum, it applies a **single-shot correction to the root cause of the numerical breakdown** in the simulation.

## The problem

The electric field integral equation (EFIE) is a workhorse of full-wave simulation, but it **breaks down at low frequencies**: the system becomes severely ill-conditioned and the solution loses accuracy. The usual workaround is to combine separate low-frequency (quasi-static) and high-frequency (full-wave) solvers and stitch their results together. That adds complexity and can introduce errors at the transition.

## Approach

- Identified the **root mathematical cause** of the breakdown, rather than treating symptoms with special basis functions or preconditioners
- Derived a method that finds the **solution of the original EFIE at any frequency where it breaks down**, whether from low frequencies or dense discretization. It is equally rigorous where the EFIE does not break down, and it is **independent of the basis functions** used.
- Showed, theoretically and numerically, that the solution at "low-frequency" breakdown can be **dominated by full-wave effects**, not just static or quasi-static physics
- Applicable to other integral equations and numerical methods for Maxwell's equations

## Results

{% include figure popup=true image_path="/assets/images/projects/em-breakdown-correction/tap2014-fig04-sphere-rcs-1hz-and-1ghz.jpg" alt="Bistatic RCS of a conducting sphere at 1 Hz and 1 GHz" caption="Bistatic radar cross section of a 1 m conducting sphere. At 1 Hz (a) the proposed method matches the analytical Mie series while the traditional EFIE breaks down; at 1 GHz (b) both agree. *Zhu, Omar & Jiao, IEEE TAP 2014, Fig. 4.*" %}

{% include figure popup=true image_path="/assets/images/projects/em-breakdown-correction/tap2014-fig05-multiscale-inductor-efie-error.jpg" alt="Multiscale inductor and EFIE error vs frequency" caption="A multiscale loop inductor spanning seven orders of magnitude in geometric scale (1 nm strips in a 1 cm structure), and the error of the traditional EFIE from 1 Hz to 20 GHz. The breakdown persists even where full-wave effects matter. *Zhu, Omar & Jiao, IEEE TAP 2014, Fig. 5.*" %}

{% include figure popup=true image_path="/assets/images/projects/em-breakdown-correction/emc2013-fig02-multiscale-capacitor-error-vs-frequency.jpg" alt="Multiscale capacitor and solver error vs frequency" caption="A multiscale capacitor and the error of a traditional full-wave solver from 1 Hz to 10¹² Hz, revealing a wide frequency band where the conventional solution is unknown. *Zhu, Omar & Jiao, IEEE EMC 2013, Fig. 2.*" %}

{% include figure popup=true image_path="/assets/images/projects/em-breakdown-correction/tap2014-fig03-parallel-plate-capacitor.jpg" alt="Parallel-plate capacitor test geometry" caption="Parallel-plate capacitor test case driven by a delta-gap source, used to validate capacitance extraction at breakdown frequencies. *Zhu, Omar & Jiao, IEEE TAP 2014, Fig. 3.*" %}

## Impact

- One solver for both low- and high-frequency analysis, with no solver stitching
- Validated on inductance, capacitance, and radar cross-section extraction, plus a multiscale example spanning **seven orders of magnitude** in geometric scale
- Simpler, more robust broadband simulation workflows for circuits and scattering problems

## Related work

- J. Zhu, S. Omar, and D. Jiao, "Solution to the electric field integral equation when it breaks down," *IEEE Trans. Antennas and Propagation*, vol. 62, no. 8, pp. 4122–4134, Aug. 2014.
