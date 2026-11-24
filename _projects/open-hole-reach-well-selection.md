---
title: "Predicting Coiled-Tubing Open-Hole Reach for Well Selection"
excerpt: "A calibrated physics model that predicts how much of each well's open hole coiled tubing can reach (%OH), screening a 500-well field in minutes and choosing the simplest tool configuration for each well."
order: 7
toc: true
tags: [physics-informed modeling, well intervention, coiled tubing, automation]
---

**Role:** Model developer · **Organization:** SLB

## Overview

Stimulating and logging long horizontal wells relies on **coiled tubing (CT)**. Friction and buckling make the CT lock up before it reaches the end of the well, so the **percentage of open hole reached (%OH)** decides which wells are good candidates and which CT string, tractor, or agitator each one needs. I built a fast **physics model that predicts CT reach and %OH** for any well and tool configuration, using data operators already have: the directional survey, the completion schematic, and the CT string design.

## The problem

Today, reach is checked one well at a time in a commercial tubing-forces simulator, with the completion entered by hand. That is slow and error-prone, and it is impractical for screening hundreds of wells or comparing dozens of string and tractor options. Simple rules of thumb are fast but ignore the completion clearances and the string design, which control buckling and drag and therefore reach.

## Approach

- **Automated inputs:** well geometry built from 723 directional surveys and 549 completion schematics, with no manual data entry
- **Physics-based reach model:** a force balance for CT running in hole that accounts for buckling, the completion, tapered and optimized string designs, tractors, and agitators
- **Calibration and validation:** a handful of global parameters fitted on training wells against 1,064 simulated well–scenario cases, then tested on held-out wells with grouped cross-validation and bootstrap confidence intervals
- **Benchmarks:** compared with a machine-learning ensemble and simple baselines trained on the same data

## Results

- On **held-out wells**, %OH is predicted with a **mean absolute error of 2.3%** and reach with an RMSE of about 600 ft (R² = 0.98)
- Whether a well reaches TD is called correctly in **93%** of cases
- Accuracy **matches a machine-learning ensemble** trained on the same data (2.1% %OH error), while the physics model needs **no training data for new wells**
- Adding well-specific completion and string detail cuts the %OH error **more than threefold** compared with a generic model (8.3% → 2.3%)
- The calibrated parameters are stable across cross-validation folds

## Impact

- Turns a manual, well-by-well simulator exercise into **field-scale screening in minutes**: 506 wells × 25 tool configurations
- Ranks candidate wells by %OH and picks the **simplest configuration (string, tractor, agitator) that reaches TD** for each well
- Makes the drivers of reach transparent through sensitivity analysis, supporting string design and tractor selection
- Next step: validation against field CT runs with recorded depth and weight, since the current labels come from the simulator
