---
title: "Electromagnetic Multi-Casing Corrosion Evaluation"
excerpt: "Inversion-based processing of electromagnetic induction and pulsed eddy current measurements that resolves the individual thickness of four or more nested metallic pipes in oil and gas wells."
order: 3
toc: true
tags: [inversion, electromagnetics, well integrity, corrosion]
header:
  teaser: /assets/images/projects/multi-casing-corrosion/qnde2019-fig01-pec-sensitivity-map-collar.jpg
---

**Role:** Lead scientist and inventor · **Organization:** Schlumberger-Doll Research / SLB

## Overview

Wells are completed with several nested steel pipes: production tubing inside multiple casings. Corrosion of any of them threatens well integrity, CO2 storage containment, and safe abandonment. I developed **inversion-based workflows that recover the individual thickness of each pipe** from low-frequency electromagnetic measurements taken from inside the innermost pipe. The work spans multi-frequency, multi-spacing induction (non-collocated) sensors and pulsed eddy current (collocated) sensors.

## The problem

- Each additional pipe weakens and blurs the signal from pipes behind it, so pipes beyond the second are hard to resolve.
- **Tool and casing eccentering**, unknown magnetic permeability and conductivity of the steel, and casing collars all distort the measurements.
- "Ghosting", a double indication of the same defect, makes interpretation unreliable near collars.

## Approach

- **Inversion-based channel calibration** estimates unknown casing permeabilities and conductivities directly from the data, with a quality-control flag for eccentering.
- **Multi-pipe inversion** handles an arbitrary number of nested casings. The data covariance matrix gives **uncertainty estimates** for each inverted thickness.
- **Information-content analysis** using the data resolution matrix guides channel weighting, frequency selection, and sensor design.
- **Apparent-thickness preprocessing** and **2D sliding-window processing** of long logging intervals make the inversion robust to approaching anomalies and eccentering.
- **3D finite-element modeling** quantifies eccentering sensitivity and the limits of collocated vs. non-collocated sensing.

## Results

{% include figure popup=true image_path="/assets/images/projects/multi-casing-corrosion/aip2019-fig02-pec-sensor-three-casing-response.jpg" alt="PEC sensor in three nested casings and its decay response" caption="A pulsed eddy current (PEC) sensor inside three nested casings and its decaying voltage response for a 50% metal loss in each casing. Later time windows are sensitive to the outer casings. *Omar & Omeragic, AIP Conf. Proc. 2102, 2019, Fig. 2.*" %}

{% include figure popup=true image_path="/assets/images/projects/multi-casing-corrosion/qnde2019-fig01-pec-sensitivity-map-collar.jpg" alt="PEC sensitivity maps with and without a casing collar" caption="Sensitivity maps of a PEC sensor to a 1 ft defect in each of four casings, without (left) and with (right) a nearby casing collar. Collars can mask defect signatures. *Omar & Omeragic, QNDE 2019, Fig. 1.*" %}

{% include figure popup=true image_path="/assets/images/projects/multi-casing-corrosion/qnde2022-fig06-collocated-vs-noncollocated-sensitivity.jpg" alt="Collocated vs non-collocated PEC sensitivity" caption="Sensitivity of collocated and non-collocated PEC sensors to a 30% loss next to a collar on each pipe. The non-collocated sensor shows a double transmitter/receiver indication ('ghosting'). *Omar, ASME QNDE 2022, Fig. 6.*" %}

{% include figure popup=true image_path="/assets/images/projects/multi-casing-corrosion/qnde2022-fig14-advanced-processing-four-pipe-inversion.jpg" alt="Four-pipe inversion with advanced processing vs empirical processing" caption="Inverted thicknesses of four nested pipes from multi-frequency data. Advanced processing separates tool response, pipe thickness, and eccentering to give sharp results that match the truth, unlike empirical processing. *Omar, ASME QNDE 2022, Fig. 14.*" %}

{% include figure popup=true image_path="/assets/images/projects/multi-casing-corrosion/aip2017-fig11-field-log-inversion-vs-ultrasonic.jpg" alt="Two-casing field log: EM inversion vs ultrasonic" caption="Field log from a two-casing well: EM-inverted thicknesses of both casings compared with the first-casing thickness from an ultrasonic imaging tool. The periodic spikes are casing collars. *Omar & Omeragic, AIP Conf. Proc. 1806, 2017, Fig. 11.*" %}

{% include figure popup=true image_path="/assets/images/projects/multi-casing-corrosion/aip2017-fig12-field-log-three-casing-inversion.jpg" alt="Three-casing field log inversion" caption="Field log from a three-casing well: inverted thickness of each casing and total metal thickness against nominal values, with the inversion mismatch used as an eccentering indicator. *Omar & Omeragic, AIP Conf. Proc. 1806, 2017, Fig. 12.*" %}

{% include figure popup=true image_path="/assets/images/projects/multi-casing-corrosion/aip2018-fig12-field-log-collar-id-inversion.jpg" alt="Three-casing field data with automatic collar identification" caption="Three-casing field data: automatically identified collars on each casing (top), inverted thicknesses of the 1st, 2nd, and 3rd casings (middle), and inversion mismatch (bottom). *Omar & Omeragic, AIP Conf. Proc. 1949, 2018, Fig. 12.*" %}

## Impact

- EMIT-2D processing deployed on legacy hardware differentiates up to **five metallic pipe corrosion states**, generating an additional **$1M/yr** in revenue.
- Part of a portfolio of electromagnetic processing workflows deployed on SLB's digital platform for well integrity and CO2 storage monitoring.
- **6 granted US patents and 5 published patent applications** in this area; see [Publications & Patents](/publications/).

## Related work

- S. Omar, "Towards robust multi-casing evaluation using pulsed eddy current sensors," *ASME QNDE*, 2022.
- S. Omar and D. Omeragic, "Information content in pulsed eddy current measurements for evaluation of four and more metallic barriers in oil and gas wells," *QNDE*, 2019.
- S. Omar and D. Omeragic, "Casing eccentering sensitivity of pulsed eddy current sensors in multiple-casing corrosion analysis," *AIP Conf. Proc.* 2102, 2019.
- S. Omar and D. Omeragic, "Use of apparent thickness for preprocessing of low-frequency electromagnetic data in inversion-based multibarrier evaluation workflow," *AIP Conf. Proc.* 1949, 2018.
- S. Omar and D. Omeragic, "Inversion-based workflow for oilfield nested multicasing evaluation using electromagnetic low-frequency measurements," *AIP Conf. Proc.* 1806, 2017.
