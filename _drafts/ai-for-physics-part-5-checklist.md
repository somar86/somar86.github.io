---
# To publish: move to _posts/YYYY-MM-DD-ai-for-physics-part-5-checklist.md
title: "AI for Physics-Based Problems, Part 5: A Practical Checklist"
excerpt: "The final part of the series turns six patterns for combining AI and physics into seven questions to ask at the start of any AI-for-physics project, and closes with the question that ties them together: where should the physics live?"
tags: [AI, physics-informed ML, inversion, edge AI, electromagnetics]
series: ai-for-physics
part: 5
header:
  teaser: /assets/images/projects/udar-look-ahead-inversion/fig02-look-ahead-inversion-workflow.png
---

Over the previous four parts, I set up the problem and described six patterns for combining AI with physics-based inversion:

- [Part 1](/blogs/ai-for-physics-based-problems/) set the stage: why physics problems resist plain supervised learning, and the regularized inversion that every pattern builds on.
- [Part 2](/blogs/ai-for-physics-part-2-fast-simulators/): make the simulator fast, then let it teach (Pattern 1), and learn the inverse when speed is the bottleneck (Pattern 2).
- [Part 3](/blogs/ai-for-physics-part-3-physics-as-referee/): blend lab, simulation, and field data from the start (Pattern 3), and keep the physics in the loop as the referee (Pattern 4).
- [Part 4](/blogs/ai-for-physics-part-4-generative-models/): use AI to discover physics, not only to approximate it (Pattern 5), and use generative models for problems with many answers (Pattern 6).

This final part turns them into the checklist I use in practice.

{% include series-nav.html %}

## A practical checklist

When I start a new AI-for-physics project, I work through these questions:

1. **What exactly is the bottleneck?** Speed, missing labels, unknown physics, or deployment hardware? The answer determines which pattern applies.
2. **Is the simulator fast and faithful enough?** If not, fix that first. Everything downstream inherits its errors.
3. **Does the training data look like the field?** Model the measurement chain, noise, and calibration, not just ideal physics.
4. **How will a wrong answer be detected?** Plan for a physics residual check or a quality-control flag from day one.
5. **What uncertainty does the user need?** A single number is rarely enough for a high-stakes decision.
6. **Where will it run?** Edge and downhole hardware may require quantization, smaller architectures, and per-layer precision choices.
7. **Who needs to trust it?** Involve domain experts early. Their intuition is the best test set you have.

## Closing thoughts

The most successful projects I have been part of did not ask "can AI replace the physics?" They asked "**where should the physics live?**" Sometimes it lives in the simulator that generates the training data, sometimes in the features, sometimes in a residual check that referees the network, and sometimes in a closed-form equation that the data helped reveal. Treating AI and physics as partners rather than competitors is what turns a promising prototype into a tool that engineers use every day.

*If you are working on similar problems, I would be glad to connect on [LinkedIn](https://www.linkedin.com/in/saadomar/). For details of the work described here, see my [projects](/projects/) and [publications](/publications/).*
