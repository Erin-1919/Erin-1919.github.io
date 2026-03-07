# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Personal academic website for Mingke (Erin) Li, a postdoctoral scholar at the University of Calgary. The site covers research, blog posts, a gallery, and CV. Built with Jekyll and hosted on GitHub Pages at `Erin-1919.github.io`.

## Build & Serve

```bash
bundle install          # install dependencies (first time)
bundle exec jekyll serve  # local dev server at http://localhost:4000
bundle exec jekyll build  # build static site to _site/
```

Requires Ruby and Bundler. Jekyll version ~> 4.2.0.

## Architecture

- **Theme**: Custom minimal theme (not a gem-based theme). Layout/styling is entirely in this repo.
- **Layouts**: `_layouts/default.html` is the base. `page`, `post`, `home`, `gallery`, `archive`, `embed` extend it.
- **Styling**: SASS files in `_sass/` compiled via `assets/css/`. The `show_frame` config toggle switches between `frame.css` and `index.css`. Currently `show_frame: true`.
- **Math**: KaTeX (bundled in `assets/katex/`) enabled per-page via `mathjax: true` in front matter.
- **Navigation**: Defined explicitly in `_config.yml` under `navigation` (not auto-generated from pages).
- **Blog**: `blog.md` uses a tabbed layout (JS-based tabs) grouping posts by year range. Posts are in `_posts/` following Jekyll's `YYYY-MM-DD-title.md` naming.
- **Research page**: `research.md` is a large single markdown file with publications, presentations, and abstracts.
- **Gallery**: `gallery.md` uses the `gallery` layout.
- **CV**: Links to a PDF at `assets/pdf/Mingke_Li_CV_2026.pdf`.
- **Pagination**: `jekyll-paginate` with 10 posts per page, path `/blog/page:num/`.

## Adding a Blog Post

Create a file in `_posts/` named `YYYY-MM-DD-title.md` with front matter:

```yaml
---
title: "Post Title"
layout: post
---
```

Add `mathjax: true` to front matter if the post uses math notation.

The blog page groups posts into year-range tabs. If adding posts beyond the current ranges, update the tab buttons and filters in `blog.md`.

## Key Config (`_config.yml`)

- `permalink: /:title/` - URLs use post title only (no date path)
- `excerpt_separator: "\n\n\n"` - triple newline separates excerpts
- `show_excerpts: false` - excerpts not shown on listing pages
- External links (email, GitHub, ResearchGate, LinkedIn) are in the `external` section

## Plugins

`jekyll-feed`, `jemoji`, `jekyll-seo-tag`, `jekyll-paginate` - all declared in both `_config.yml` and `Gemfile`.
