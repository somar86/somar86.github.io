---
title: "Projects"
permalink: /projects/
author_profile: true
---

A selection of projects spanning subsurface imaging, computational electromagnetics, AI, computer vision, and workflow automation.

{% assign projects = site.projects | sort: "order" -%}
{% for project in projects -%}
- **[{{ project.title }}]({{ project.url | relative_url }})**: {{ project.excerpt | strip_html | strip_newlines | strip }}
{% endfor %}
