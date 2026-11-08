---
title: "Look-Ahead Inversion: Imaging Ahead of the Bit"
excerpt: "Inventor and developer of the industry's first look-ahead inversion of ultra-deep resistivity measurements, imaging up to 70 ft ahead of the tool."
order: 2
toc: true
tags: [inversion, electromagnetics, look-ahead, drilling]
header:
  teaser: /assets/images/projects/udar-look-ahead-inversion/rn2022-fig15-two-sand-channels-geosphere-look-ahead.jpg
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

## Patent figures

These figures are from the published patent ([WO 2024/091651 A1](https://patents.google.com/patent/WO2024091651A1/en), granted as [US 12,467,353 B2](https://patents.google.com/patent/US12467353B2/en)).

{% include figure popup=true image_path="/assets/images/projects/udar-look-ahead-inversion/fig01-look-behind-around-ahead-zones.png" alt="Tool layout and look-behind, look-around, and look-ahead zones" caption="Tool layout, with a tilted transmitter near the bit and receivers behind it, defining the look-behind, look-around, and look-ahead zones and the look-ahead window in front of the transmitter. *US 12,467,353 B2, FIG. 1.*" %}

{% include figure popup=true image_path="/assets/images/projects/udar-look-ahead-inversion/fig02-look-ahead-inversion-workflow.png" alt="Look-ahead inversion workflow flowchart" caption="The real-time workflow: a 1D look-around inversion seeds an optional 2D pixel-based look-around step, followed by continually running 2D pixel-based look-ahead inversions as new data arrive. *US 12,467,353 B2, FIG. 2.*" %}

{% include figure popup=true image_path="/assets/images/projects/udar-look-ahead-inversion/fig03-fault-case-look-ahead-result.png" alt="Fault case: true model and look-around vs look-ahead inversions" caption="Fault case: a three-layer formation with an abrupt resistivity break (top). The 2D look-ahead inversion predicts the break ahead of the transmitter, which the 1D look-around inversion cannot. *US 12,467,353 B2, FIG. 3.*" %}

{% include figure popup=true image_path="/assets/images/projects/udar-look-ahead-inversion/fig04-sand-channel-look-ahead-result.png" alt="Look-ahead imaging of two staggered sand channels" caption="Two staggered sand channels imaged every 5 ft as the tool advances, with the true model at the bottom. The end of the upper sand is predicted ahead of the bit. *US 12,467,353 B2, FIG. 4.*" %}

## Results

Synthetic case studies from the research note: S. Omar, J. Liu, and L. Liang, *2D look-ahead pixel-based inversion workflow for real-time processing of ultra-deep directional resistivity measurements in high-angle and horizontal wells*, 2022. Look-ahead distances are measured ahead of the transmitter.

{% include figure popup=true image_path="/assets/images/projects/udar-look-ahead-inversion/rn2022-fig08-look-around-look-ahead-workflow.jpg" alt="Look-around and look-ahead workflow" caption="The real-time workflow: a 1D look-around step, an optional 2D look-around step, then continually running 2D pixel-based look-ahead inversions as new measurements arrive. *Omar, Liu & Liang, 2022, Fig. 8.*" %}

{% include figure popup=true image_path="/assets/images/projects/udar-look-ahead-inversion/rn2022-fig09-fault-look-ahead-new-workflow.jpg" alt="Low-contrast fault imaged ahead of the transmitter" caption="A low-contrast fault: the new look-around/look-ahead workflow adds about 20 ft of look-ahead compared with the original workflow. *Omar, Liu & Liang, 2022, Fig. 9.*" %}

{% include figure popup=true image_path="/assets/images/projects/udar-look-ahead-inversion/rn2022-fig15-two-sand-channels-geosphere-look-ahead.jpg" alt="Two staggered sand channels imaged ahead of the transmitter" caption="Two staggered sand channels: the end of the upper sand is predicted about 30 ft ahead of the transmitter, and the lower sand is detected once the transmitter is above it (true model at bottom right). *Omar, Liu & Liang, 2022, Fig. 15.*" %}

{% include figure popup=true image_path="/assets/images/projects/udar-look-ahead-inversion/rn2022-fig18-sand-channel-la3d-window-selection.jpg" alt="Old vs optimized data-window selection" caption="Old (left) and optimized (right) data-window selection: the optimized window predicts the end of the reservoir about 38 ft ahead of the transmitter. *Omar, Liu & Liang, 2022, Fig. 18.*" %}

{% include figure popup=true image_path="/assets/images/projects/udar-look-ahead-inversion/rn2022-fig21-water-coning-look-ahead.jpg" alt="Water cone imaged ahead of the transmitter" caption="Water coning: a water cone rising toward the well is imaged about 30–35 ft ahead of the transmitter, with and without the deepest receiver spacing. *Omar, Liu & Liang, 2022, Fig. 21.*" %}

{% include figure popup=true image_path="/assets/images/projects/udar-look-ahead-inversion/rn2022-fig23-realistic-fault-look-ahead.jpg" alt="Realistic normal fault imaged ahead of the transmitter" caption="A realistic normal fault (30 ft throw, 68° dip): the fault is predicted about 40 ft ahead of the transmitter. *Omar, Liu & Liang, 2022, Fig. 23.*" %}

## Impact

- Ahead-of-the-bit sensing and imaging for proactive geosteering and drilling-risk reduction
- Part of the ultra-deep resistivity imaging portfolio deployed on SLB's digital platform

## Related work

- **Patent WO-2024091651-A1:** Look-around/look-ahead pixel-based inversion workflow for real-time prediction ahead of the bit in horizontal and high-angle wells.
- See also: [3D inversion of ultra-deep resistivity measurements](/projects/udar-3d-inversion/)
