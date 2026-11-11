# somar86.github.io: editing guide

Source for **https://somar86.github.io**. This file explains how the site is put together and how to change it. It is not published on the site.

## How the site works

- Every page is a **Markdown** (`.md`) file with a short settings header called **front matter**.
- **Jekyll** turns those files into HTML using the **Minimal Mistakes** theme. The theme's files are copied into this repo, so the site does not depend on anything outside it.
- **GitHub Pages** runs Jekyll automatically every time you push to `master`. The live site updates 1–2 minutes later. Progress and errors appear in the repo's **Actions** tab, under "pages build and deployment". If a build fails, the live site keeps the previous version.
- Nothing builds on this computer. See [Previewing locally](#previewing-locally).

## Where everything is

| What you see on the site | URL | File to edit |
|---|---|---|
| Home (About) page | `/` | `index.md` |
| Top menu | every page | `_data/navigation.yml` |
| Left sidebar: photo, bio, links | every page | `_config.yml`, `author:` section |
| Site title and description | browser tab, search results | `_config.yml`, top section |
| Projects list | `/projects/` | `_pages/projects.md` (built automatically from `_projects/`) |
| One project | `/projects/<file-name>/` | `_projects/<file-name>.md` |
| Blogs list | `/blogs/` | `_pages/blogs.md` (built automatically from `_posts/`) |
| One blog | `/blogs/<file-name>/` | `_posts/YYYY-MM-DD-<file-name>.md` |
| Unpublished drafts | not on the site | `_drafts/` |
| Blog series box | top of each series part | `_data/series.yml` and `_includes/series-nav.html` |
| Publications & patents | `/publications/` | `_pages/publications.md` |
| CV | `/cv/` | `_pages/cv.md` |
| Images | | `assets/images/` (project figures in `assets/images/projects/<project>/`, profile photo `assets/images/bio-photo.jpg`) |
| Extra code in every page's `<head>` (MathJax) | | `_includes/head/custom.html` |

**Files you can leave alone.** These belong to the theme: `_layouts/`, `_sass/`, `assets/css/`, `assets/js/`, `_data/ui-text.yml`, and everything in `_includes/` except the two files named above. Edit them only if you want to change how *every* page looks. These are leftovers from the theme's own repository and are not used by your site: `.github/`, `Rakefile`, `package.json`, `staticman.yml`, `Gemfile`. Keep `LICENSE`: it is the theme's license, which asks that it stay with copies of the theme.

## Anatomy of a content file

Every content file starts with front matter between two `---` lines, followed by the text in Markdown:

```markdown
---
title: "Real-Time Physics Inversion on 8-bit Integer NPUs"
excerpt: "One- or two-sentence summary shown in lists and link previews."
order: 4
toc: true
tags: [AI, edge computing, quantization, inversion]
header:
  teaser: /assets/images/projects/npu-int8-inversion/icad2025-fig01-multitask-learning-architecture.jpg
---

**Role:** Project lead · **Organization:** SLB

## Overview

Text in Markdown...
```

| Field | Used in | What it does |
|---|---|---|
| `title` | everything | Page heading and browser-tab title |
| `excerpt` | projects, blogs | Summary shown on the Projects/Blogs lists, the home page, and LinkedIn/social previews |
| `order` | projects | Position on the Projects page (1 = first) |
| `tags` | projects, blogs | Tags shown at the bottom of the page (see [Known issues](#known-issues)) |
| `toc` | any page | `true` adds a table of contents on the right, built from the `##` headings |
| `mathjax` | any page | `true` turns on LaTeX equations |
| `header: teaser:` | projects, blogs | Thumbnail image used in related-post lists and previews |
| `permalink` | `_pages/`, `index.md` | The page's URL (projects and blogs get theirs from the file name) |
| `redirect_from` | any page | An old URL that should forward to this page, e.g. `redirect_from: /articles/` |
| `series`, `part` | blogs | Puts a blog in a series (see [Start a new blog series](#start-a-new-blog-series)) |

Front matter rules:
- It must be the very first thing in the file, between two lines of exactly `---`.
- Indent with **spaces, never tabs**. The two spaces before `teaser:` matter.
- Put text in double quotes, especially if it contains a colon (`title: "Part 2: Fast Simulators"`). If the text itself contains double quotes, use single quotes around it instead.

## Common tasks

### Change text on a page

Find the file in the table above, edit the Markdown, then commit and push.

### Add a project

1. Copy an existing file in `_projects/`, for example `npu-int8-inversion.md`, and rename it. The file name becomes the URL: `_projects/my-new-project.md` → `/projects/my-new-project/`. Use lowercase and hyphens, no spaces.
2. Edit the front matter: `title`, `excerpt`, `order`, `tags`, `header: teaser:`.
3. Put its images in a new folder, `assets/images/projects/my-new-project/`.
4. Write the page. Existing projects use these sections: Overview, The problem, Approach, Results, Impact, Related work.

The project appears on `/projects/` automatically, sorted by `order`.

### Reorder projects

Change the `order:` number in each project's front matter. The current order runs from 1 (`udar-3d-inversion`) to 11 (`license-plate-recognition-parking`). Two projects with the same number are fine, but their relative order is then unpredictable.

### Add a publication or patent

Edit the matching section of `_pages/publications.md` and copy the format of the item next to it. Markdown renumbers numbered lists automatically, so you can insert an item anywhere without fixing the numbers below it. To link the item to a project, end it with `[→ project](/projects/<project-file-name>/)`.

### Update the CV

Edit `_pages/cv.md`. Each job is a `###` heading followed by an italic line (`*Place · Dates*`) and a paragraph or bullet list.

### Write and publish a blog

1. Copy `_drafts/blog-template.md` to `_drafts/my-blog.md` and write it. Its comments explain every field. Files in `_drafts/` are **never published**, so you can work on them over several commits.
2. To publish, **move** the file to `_posts/` and add the date in front of the name: `_posts/2026-12-01-my-blog.md`. The URL becomes `/blogs/my-blog/`.
3. Commit and push. The blog appears on `/blogs/` and in the home page's "Latest blogs" list.

**About dates:** a post dated in the future is hidden when the site is built, and the site is only built when you push. So a post dated December 1 does not appear on December 1 by itself. It appears with your first push on or after that date.

**For the "AI for Physics-Based Problems" series:** move each remaining part from `_drafts/` to `_posts/`, adding the date to the name and keeping the rest of the name unchanged, because later parts link to that URL. Delete the copy left in `_drafts/` so there is only one version to edit.

### Add a figure

Put the image in `assets/images/...`, then add this line to the page, on its own line with blank lines around it:

```liquid
{% include figure popup=true image_path="/assets/images/projects/my-project/fig01-name.jpg" alt="Short description" caption="Caption text. *Author et al., Venue Year.*" %}
```

`popup=true` lets readers click the image to enlarge it.

### Add equations

Set `mathjax: true` in the front matter. Inline math uses double dollar signs, `$$E = mc^2$$`. For a displayed equation, put `$$` on its own line before and after it.

### Change the top menu

Edit `_data/navigation.yml`. Each entry is a `title` and a `url`. Entries appear in file order.

### Change the sidebar photo, bio, or links

Edit the `author:` section of `_config.yml`:
- `avatar`: replace `assets/images/bio-photo.jpg` with a new photo of the same name, or point this to a new file.
- `bio`, `location`, `email`: plain text.
- `links`: each has a `label`, an `icon` (a [Font Awesome](https://fontawesome.com/search?o=r&m=free) name such as `fab fa-linkedin`), and a `url`.

The footer has its own `footer: links:` list in the same file. Its entries have no `url` yet, so the footer currently shows none of them.

### Change the colors

Set `minimal_mistakes_skin` near the top of `_config.yml` to one of the names listed in the comment beside it, such as `"air"`, `"mint"`, or `"dark"`.

### Start a new blog series

1. Add an entry to `_data/series.yml` with a key, a `title`, and the list of part titles.
2. In each part's front matter, add `series: <key>` and `part: <number>`.
3. In each part's text, add `{% include series-nav.html %}` where the box listing all parts should go, and `{% include series-nav.html next=true %}` where the "Next in the series" line should go.

Published parts become links automatically, and unpublished ones are marked "coming soon".

## Markdown quick reference

| You type | You get |
|---|---|
| `## Heading` / `### Subheading` | Section headings (`##` headings feed the table of contents) |
| `**bold**`, `*italic*` | **bold**, *italic* |
| `[text](/projects/udar-3d-inversion/)` | A link to another page on the site |
| `[text](https://example.com)` | A link to another website |
| `- item` | Bulleted list |
| `1. item` | Numbered list |
| a blank line | A new paragraph (a single line break is ignored) |
| `---` on its own line, with blank lines around it | A horizontal rule |
| `` `code` `` | `code` |

Tables use `|` between columns, with a `|---|---|` line under the header row, as in this file.

## Publishing workflow

1. Edit the files, in VS Code, any text editor, or directly on github.com with the pencil icon.
2. Commit and push to `master`.
3. Wait 1–2 minutes. Check the **Actions** tab if you want to see the build. Then reload the page; Ctrl+F5 skips the browser's cache.

If the build fails, open the failed run in the Actions tab. The log names the file and usually the line that caused the error.

## Things that commonly go wrong

- **Capital letters in file names.** Windows treats `Fig1.jpg` and `fig1.jpg` as the same file, but the live site does not. A picture that shows up locally but is broken online usually has a capitalization mismatch. Use lowercase file names throughout.
- **Spaces in file names.** Use hyphens instead: `fig01-field-log.jpg`.
- **Renaming a file changes its URL.** Search the repo for the old name and update every link to it. For links you can't edit, such as LinkedIn posts you have already shared, add `redirect_from: /old/url/` to the renamed page's front matter so the old address forwards to the new one.
- **A mistake in `_config.yml` breaks the whole site.** It is YAML: keep the indentation exactly as it is and use spaces, not tabs.
- **A post that doesn't appear.** Check that it is in `_posts/` (not `_drafts/`), that its name starts with `YYYY-MM-DD-`, and that the date is not in the future.

## Known issues

- **Tag links lead to a missing page.** Tags at the bottom of blogs and projects link to `/tags/`, which does not exist, so readers get a "page not found" error. The fix is a small `_pages/tags.md` page, or set `show_taxonomy: false` in `_config.yml` to hide the tags.

## Previewing locally

Local preview is not set up. Ruby is not installed on this computer, and `Gemfile` refers to the theme's `minimal-mistakes-jekyll.gemspec`, which was deleted from the repo. Setting it up means installing Ruby and replacing the `Gemfile` with one that uses the `github-pages` gem. Until then, pushing to GitHub and checking the live site is the way to see changes.
