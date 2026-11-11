---
# HOW TO PUBLISH A BLOG
# 1. Copy this file to _posts/ and rename it YYYY-MM-DD-short-title.md
#    (e.g. _posts/2026-11-15-physics-informed-inversion.md).
#    The date in the filename is the publication date; the URL becomes /blogs/short-title/.
# 2. Edit the front matter below and write the blog in Markdown.
# 3. Put images in assets/images/blogs/ and reference them as shown below.
# 4. Commit and push; the blog appears on /blogs/ and on the home page.
# Files in _drafts/ are never published, so you can keep work-in-progress here.
title: "Blog Title"
excerpt: "One- or two-sentence summary shown in blog lists and link previews."
tags: [inversion, AI]
toc: true          # table of contents on the right; set false for short blogs
mathjax: true      # enables LaTeX equations; set false if not needed
header:
  teaser: /assets/images/blogs/example.jpg   # optional preview image
---

Opening paragraph: what problem this blog addresses and why it matters.

## Background

Regular Markdown works: **bold**, *italic*, [links](https://example.com), lists, and tables.

| Method | Complexity |
|--------|------------|
| Direct dense solve | O(N³) |
| Fast direct solver | O(N) |

## Equations

Inline math uses double dollar signs: $$\nabla \times \mathbf{E} = -j\omega\mu\mathbf{H}$$.

Display math goes on its own lines:

$$
\min_{\mathbf{m}} \; \|\mathbf{W}_d\,(\mathbf{d} - F(\mathbf{m}))\|^2 + \lambda \|\mathbf{W}_m \mathbf{m}\|^2
$$

## Figures

{% include figure popup=true image_path="/assets/images/blogs/example.jpg" alt="Short description of the image" caption="Figure caption. *Source, if any.*" %}

## Code

```python
import numpy as np

def misfit(d_obs, d_pred):
    return np.linalg.norm(d_obs - d_pred) ** 2
```

## Conclusion

Key takeaways.
