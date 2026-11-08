---
title: "Look-Ahead Inversion: Imaging Ahead of the Bit"
excerpt: "Inventor and developer of the industry's first look-ahead inversion of ultra-deep resistivity measurements, imaging up to 70 ft ahead of the tool."
order: 2
toc: true
tags: [inversion, electromagnetics, look-ahead, drilling]
header:
  teaser: /assets/images/projects/udar-look-ahead-inversion/fig04-sand-channel-look-ahead-result.png
---

**Role:** Inventor and lead developer · **Organization:** Schlumberger-Doll Research / SLB

## Overview

I invented and developed the industry's **first look-ahead inversion of ultra-deep resistivity measurements**. It images the formation **up to 70 ft ahead of where the tool currently is**, so drillers see what is coming instead of reacting after the bit has already crossed it.

## The problem

Logging-while-drilling sensors sit behind the bit, so conventional interpretation describes rock the bit has already drilled through. In horizontal and high-angle wells, unexpected boundaries, faults, or fluid contacts ahead of the bit can mean exiting the reservoir, drilling hazards, or costly sidetracks.

## Approach

- **Multistep pixel-based workflow:** a 1D model-based look-around inversion, optionally refined by a 2D pixel-based look-around inversion, characterizes the formation already drilled.
- **Warm-started look-ahead:** the look-around structure jump-starts continually running **2D pixel-based look-ahead inversions** over a data window that shifts with each new measurement. This maximally extracts the look-ahead sensitivity of the tilted-transmitter, ultra-deep directional resistivity measurements.
- **Real-time workflow** for horizontal and high-angle wells, supporting in-situ decisions such as landing, stopping, or steering away from hazards.

## Figures

These figures are from the published patent ([WO 2024/091651 A1](https://patents.google.com/patent/WO2024091651A1/en), granted as [US 12,467,353 B2](https://patents.google.com/patent/US12467353B2/en)).

{% include figure popup=true image_path="/assets/images/projects/udar-look-ahead-inversion/fig01-look-behind-around-ahead-zones.png" alt="Tool layout and look-behind, look-around, and look-ahead zones" caption="Tool layout, with a tilted transmitter near the bit and receivers behind it, defining the look-behind, look-around, and look-ahead zones and the look-ahead window in front of the transmitter. *US 12,467,353 B2, FIG. 1.*" %}

{% include figure popup=true image_path="/assets/images/projects/udar-look-ahead-inversion/fig02-look-ahead-inversion-workflow.png" alt="Look-ahead inversion workflow flowchart" caption="The real-time workflow: a 1D look-around inversion seeds an optional 2D pixel-based look-around step, followed by continually running 2D pixel-based look-ahead inversions as new data arrive. *US 12,467,353 B2, FIG. 2.*" %}

{% include figure popup=true image_path="/assets/images/projects/udar-look-ahead-inversion/fig03-fault-case-look-ahead-result.png" alt="Fault case: true model and look-around vs look-ahead inversions" caption="Fault case: a three-layer formation with an abrupt resistivity break (top). The 2D look-ahead inversion predicts the break ahead of the transmitter, which the 1D look-around inversion cannot. *US 12,467,353 B2, FIG. 3.*" %}

{% include figure popup=true image_path="/assets/images/projects/udar-look-ahead-inversion/fig04-sand-channel-look-ahead-result.png" alt="Look-ahead imaging of two staggered sand channels" caption="Two staggered sand channels imaged every 5 ft as the tool advances, with the true model at the bottom. The end of the upper sand is predicted ahead of the bit. *US 12,467,353 B2, FIG. 4.*" %}

## Impact

- Ahead-of-the-bit sensing and imaging for proactive geosteering and drilling-risk reduction
- Part of the ultra-deep resistivity imaging portfolio deployed on SLB's digital platform

## Related work

- **Patent WO-2024091651-A1:** Look-around/look-ahead pixel-based inversion workflow for real-time prediction ahead of the bit in horizontal and high-angle wells.
- See also: [3D inversion of ultra-deep resistivity measurements](/projects/udar-3d-inversion/)
