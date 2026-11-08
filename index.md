---
layout: single
title: "About"
author_profile: true
permalink: /
---

I am a computational research leader with 15+ years of experience delivering **physics-informed AI, HPC optimization, and large-scale computational solutions** in the energy and semiconductor industries. I lead AI/ML portfolios end to end, from ideation and problem framing to model deployment and monitoring with CI/CD, integrated with digital twins and operational workflows.

I am currently a **Data Science Champion at SLB Reservoir Performance HQ** in Cambridge, MA, where I lead a cross-functional team of domain experts and data scientists in Boston and Paris. Before that, I was a Principal Scientist and Computational Scientist at **Schlumberger-Doll Research**. I received my PhD from **Purdue University**, where I developed fast full-wave electromagnetic solvers for integrated circuits.

## Highlights

- **20+ patents** and peer-reviewed publications in IEEE journals and industry symposia
- Recognized by the **US National Academy of Engineering** (Frontiers of Engineering, 2019) as one of the top 100 engineers in the USA
- **SLB GoldAward** for Lab-to-Commercialization Success (2025)
- **IEEE Antennas & Propagation Society Doctoral Research Award** (2014)
- Digital solutions I developed are deployed on SLB's digital platform, generating **millions of dollars in yearly revenue**
- President of the Boston Chapter of the **Society of Petrophysicists and Well Log Analysts (SPWLA)**

## Areas of expertise

- **AI/ML:** physics-informed ML, deep learning (CNNs, Transformers, diffusion models), DNN regression on GPUs and NPUs, uncertainty quantification
- **Computational modeling:** inversion and imaging, semi-analytical and finite-element methods, integral equations, fast solvers, digital twins
- **Platforms:** Python (PyTorch, TensorFlow, JAX), MATLAB, C++/Fortran, Docker/Kubernetes, cloud (GCP, Azure, AWS)

## Latest articles

{% if site.posts.size > 0 -%}
{% for post in site.posts limit:3 -%}
- **[{{ post.title }}]({{ post.url | relative_url }})** ({{ post.date | date: "%B %-d, %Y" }}): {{ post.excerpt | strip_html | strip_newlines | strip | truncate: 180 }}
{% endfor %}

[All articles →](/articles/)
{%- else -%}
Technical articles are coming soon on the [Articles](/articles/) page.
{%- endif %}

See my [projects](/projects/), [articles](/articles/), [publications](/publications/), and [CV](/cv/).
