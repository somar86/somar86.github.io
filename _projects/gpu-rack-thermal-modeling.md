---
title: "Thermal Modeling of Liquid- and Air-Cooled GPU Racks"
excerpt: "A verified 3D finite-volume thermal model of a 72-GPU rack with hybrid direct-to-chip liquid and air cooling, plus closed-form design formulae that rank the levers keeping GPUs below their temperature limit."
order: 7
toc: true
mathjax: true
tags: [thermal modeling, data centers, finite volume, digital twins, HPC]
header:
  teaser: /assets/images/projects/gpu-rack-thermal-modeling/rack-section-through-hottest-gpu.png
---

**Role:** Formulation, implementation, and verification · **Organization:** SLB

## Overview

AI-training racks such as the NVIDIA GB200/GB300 NVL72 pack 72 GPUs, each dissipating about 1.4 kW, into nine compute trays. **Direct-to-chip (D2C) cold plates** remove most of that heat, but the rest flows into the trays and the air between them. I developed a **3D finite-volume thermal model** of the full rack that couples conduction in every tray with the air flowing through every gap, and derived **closed-form formulae** from it that show which design levers keep the GPUs below their temperature limit.

## The problem

With 80% of the GPU heat going to liquid, the air still has to carry about 20 kW per rack. As the air crosses a tray it heats up, so GPUs on the outlet side see warmer air than those on the inlet side. Whether a design stays under the limit depends on how heat spreads in the trays, how well it transfers to the air, and how the air heats up from inlet to outlet. Full CFD answers this for one design at a time and is too slow for exploring the design space. Designers need a fast, verified model that ranks the levers and tells them how far each one must move.

## Approach

- **Conjugate heat transfer on one grid:** trays and air on a single finite-volume grid, with upwind advection in the air gaps and a wall-to-bulk heat-transfer coefficient at every solid–air face
- **Fast solves:** the steady state is one sparse linear solve (about 10 s). Heat-up uses implicit, unconditionally stable time stepping
- **Closed-form reduced model** derived from the 3D formulation. To leading order, the peak GPU-footprint temperature is

  $$T_\text{peak} \approx T_\text{in} + \xi\,\Delta T_g + \varphi\,\frac{q}{h_\Sigma}$$

  where $$\Delta T_g$$ is the air temperature rise across a gap, $$\xi \approx 0.75$$ places the peak under the outlet-side GPUs, $$q/h_\Sigma$$ is the film temperature drop, and $$\varphi$$ measures how concentrated the heat stays under the GPU
- **Sensitivity and design studies:** one-at-a-time tornado rankings, single-lever scans, and alternative airflow layouts
- **Formulation review:** reviewing an earlier version of the model found that the solid–air heat-transfer coefficient was applied in series with an extra air half-cell. The corrected wall-to-bulk formulation is now in the model

## Verification

- Reproduces the **MATLAB PDE Toolbox** solution to **0.016 K** over a 0–300 s heat-up
- Matches **exact gap-conduction and heat-spreading solutions** to **0.09 K**
- The **closed-form formulae** agree with the full 3D model to within **2 K** across 55 cases
- Energy balance closes to about **10⁻⁸ W** at steady state

## Results

{% include figure popup=true image_path="/assets/images/projects/gpu-rack-thermal-modeling/rack-section-through-hottest-gpu.png" alt="Temperature section through the rack along the airflow" caption="Steady-state temperature on a vertical section through the hottest GPU: nine trays (thin bands) separated by air gaps, with air entering from the left. The air heats up as it crosses each tray, so the GPUs on the outlet side run hottest." %}

- **Base case** (80% D2C, air at 1.5 m/s from one side): the peak GPU-footprint temperature reaches **120 °C**, above the 100 °C limit. The outlet-side GPUs run about **20 K hotter** than the inlet-side ones because their air has already picked up the inlet-side heat
- **Air from both ends, same total airflow:** the peak falls by **7 K** to 113 °C, and both GPU columns run at the same temperature
- **Air from both ends at the same speed** (twice the air): the peak falls to **95 °C**, below the limit. Most of that gain comes from the extra air, not the layout
- **Biggest levers** on the peak temperature: air speed (61 K swing over 1–2 m/s), heat-sink film coefficient (55 K over 50–150 W/m²K), and the liquid share of GPU heat (47 K over 75–85%)
- **Targets for 100 °C:** raise the liquid share from 80% to 84%, *or* double the heat-sink film coefficient, *or* raise the air speed from 1.5 to 2 m/s
- **Heat-up:** the rack reaches 95% of its steady temperature rise in about 12 minutes

{% include figure popup=true image_path="/assets/images/projects/gpu-rack-thermal-modeling/one-side-vs-split-airflow-comparison.png" alt="Tray temperature and steady-state comparison for one-sided and split airflow" caption="Left: tray temperature along the hottest GPU row (shaded: GPU footprints). Right: peak and mean GPU-footprint temperatures and outlet air for air from one side, split flow with the same total air, and split flow at the same speed at each end." %}

## Impact

- Ranks cooling design options in seconds instead of running a CFD case for each
- Gives quantitative targets for each lever (liquid share, heat-sink performance, airflow, and layout) to keep GPUs below their limit
- Shows the trade-off between airflow layout and air volume
- Identifies what to measure next: heat-sink performance against air speed and the liquid share against coolant flow. Calibrating these inputs against CFD or rack thermocouple data will make the absolute temperatures predictive
