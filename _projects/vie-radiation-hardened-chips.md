---
title: "3D Volume Integral Formulation for Chips in Harsh Radiation Environments"
excerpt: "A new 3D volume integral formulation, built from first-principles physics, for co-designing semiconductor chips used in satellites, data centers, and other high-radiation environments."
order: 5
toc: true
tags: [computational electromagnetics, semiconductors, space electronics]
---

**Role:** Developer (PhD research) · **Organization:** Purdue University · **Funding:** NSF and Department of Defense

## Overview

I built, from scratch and from first-principles physics, a **new 3D volume integral equation (VIE) formulation** for the **co-design of semiconductor chips** that operate in harsh environments such as **satellites and other space systems, and data centers**, where high radiation and external electromagnetic fields degrade circuit performance.

## The problem

Circuits in space and other high-radiation environments are exposed to external fields that couple into on-chip interconnects and devices. Conventional circuit-extraction tools model the chip in isolation and cannot capture how external fields interact with complex, inhomogeneous 3D chip structures, so these effects are found late or designed around with costly margins.

## Approach

- Derived a **broadband volume integral formulation** directly from Maxwell's equations that models the chip together with **incident external fields**
- Handles **inhomogeneous materials** (multiple dielectrics, conductors, and substrates) in full 3D
- Supports simulation **with and without external fields** in one framework, so designers can quantify how the environment affects circuit behavior and design for it from the start

## Impact

- Enables co-design of circuits and their operating environment for VLSI satellite circuits and other radiation-exposed electronics
- Became the foundation for the [linear-complexity 3D EM solver](/projects/linear-complexity-3d-em-solver/)

## Related work

- S. Omar and D. Jiao, "A new volume integral formulation for broadband 3-D circuit extraction in inhomogeneous materials with and without external electromagnetic fields," *IEEE Trans. Microwave Theory and Techniques*, vol. 61, no. 12, pp. 4302–4312, 2013. [doi:10.1109/TMTT.2013.2285355](https://doi.org/10.1109/TMTT.2013.2285355)
