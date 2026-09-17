# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Personal academic website for Mingke Erin Li — Postdoctoral Associate at the University of Calgary and incoming Assistant Professor at the University of Guelph (from December 2026). Built with Jekyll, hosted on GitHub Pages at `Erin-1919.github.io`.

**Pushing to `master` publishes immediately.** There is no staging environment. Work on `prototype` and merge when verified.

## Build & Serve

```bash
bundle install                  # first time
bundle exec jekyll serve        # local dev at http://localhost:4000
bundle exec jekyll build        # static build to _site/
```

A passing build prints `done in N seconds` with **zero warnings and zero errors**. Treat any warning as a defect — the site currently builds clean, so a new one is something you introduced.

`jekyll serve --livereload` has been observed serving stale output after edits to `_layouts/` or `_includes/`. If a change does not appear, run `bundle exec jekyll build` in another terminal; the server then serves the fresh output.

### Toolchain constraints

- **Jekyll is pinned to `~> 3.9`** to match the GitHub Pages classic builder. Do not upgrade to 4.x; local builds would then diverge from production.
- Ruby 3.4 removed `csv`, `base64`, `logger`, and `bigdecimal` from stdlib. All four are explicit gems in the `Gemfile`. Removing any of them stops Jekyll booting.
- **Only GitHub Pages whitelisted plugins may be used**: `jekyll-email-protect`, `jekyll-redirect-from`, `jekyll-paginate`, `jekyll-feed`, `jekyll-seo-tag`. A non-whitelisted plugin is silently ignored in production.

## Architecture

**Theme**: [luost26/academic-homepage](https://github.com/luost26/academic-homepage), vendored into the repo (not a gem) and modified. Bootstrap 4, jQuery, masonry.

### Content lives in four collections

| Path | Holds | Output |
|---|---|---|
| `_publications/<year>/<slug>.md` | 37 papers, presentations, talks, theses | rendered by `publications.html`, no standalone URLs |
| `_news/YYYY-MM-DD-slug.md` | conferences, talks, awards, appointments | pages at `/news/<slug>/` |
| `_posts/YYYY-MM-DD-slug.md` | technical writing, reading notes, reflections | pages at `/<title-slug>/` |
| `_showcase/posters/*.md` | conference poster cards | rendered by `showcase.html`, no standalone URLs |

The participation test decides between `_news/` and `_posts/`: something she took part in is news, something she observed and wrote about is a post.

### Pages and layouts

Root pages: `index.html`, `publications.html`, `news.html`, `blog.html`, `showcase.html`, `cv.html` (a `redirect_to` stub pointing at the CV PDF), `404.html`.

Layouts: `default.html`, `blog_post.html`, `news.html`, `prompt.html`.

`_config.yml` assigns layouts by collection, so **content files should not declare a `layout:` key**:

```yaml
defaults:
  - scope: { path: "", type: "posts" }
    values: { layout: "blog_post" }
  - scope: { path: "", type: "news" }
    values: { layout: "news" }
```

### Site data

`_data/profile.yml` drives the whole home page: name, positions, email, social links, portrait, bio, education, experience, and a commented-out awards block. `navigation.yml` is the navbar, `display.yml` the home-page toggles and the news window, `authors.yml` the author-name bolding.

### Customisations to the upstream theme

Keep these in mind before pulling anything from upstream:

1. `_layouts/news.html` and `news.html` — added; upstream news items are headline-only with no pages.
2. `widgets/news_card.html` — branches on whether an item has a body, and links only those that do.
3. `publications.html` — rewritten as four Bootstrap pill tabs over `category`.
4. `widgets/publication_item.html` — abstract behind a `<details>` toggle; entries without a `cover` render no image at all rather than the theme's generated bubble-hash graphic.
5. `widgets/publication_card.html` — single "All publications" link in the header.
6. `widgets/experience_card.html` / `profile_card*.html` — logo `<img>` only rendered when a `logo:` is set, plus a ResearchGate branch the theme lacks.
7. `showcase.html` — GLightbox wired in.
8. `assets/css/global.css` — type scale raised (`html` 17px, `.small` 0.875em), content images capped at 32rem.

## Critical conventions

### Permalinks

`_config.yml` carries `permalink: /:title/`. **Do not remove it.** Dropping it silently rewrites every blog post URL to `/YYYY/MM/DD/slug.html` and breaks every inbound link. This has happened once. The `news` collection overrides it with its own `/news/:path/`.

### News items need an explicit `date:`

Jekyll derives dates from filenames for `_posts/` only. A `_news/` file without a `date:` key gets a zero timestamp, drops off the home page, and groups under a blank year. Always set it.

### The home news window

`display.yml` sets `news_months: 12` and `min_news: 3`. The home page shows news from the last 12 months, falling back to the 3 most recent so the block never renders empty. `site.time` is build time, so the window only advances on rebuild.

### Author bolding

Never bold names inline in `_publications/` front matter. `_data/authors.yml` bolds `Li, M.`, `Li, M.E.`, and `Mingke Erin Li`. Use whichever citation form the publication uses and do not normalise them.

### Links and paths

Site assets use **site-relative** paths (`/assets/pdf/papers/x.pdf`), never `https://Erin-1919.github.io/...`. PDFs are organised into `assets/pdf/{papers,posters,slides,thesis,cv}`.

### Math

Write `$$ ... $$`. Kramdown rewrites it to `\[ ... \]`, and both layouts configure KaTeX with `'\\['` / `'\\]'` — **doubled backslashes**, because `'\['` is not a JavaScript escape and silently collapses to `'['`, which matches nothing. KaTeX loads from a CDN on every page, so `mathjax: true` in front matter does nothing. Math can only be verified in a browser; a grep of the built HTML will not show `class="katex"`.

### Images

Resize to 1600px on the long edge before committing, and use JPEG for photographs. CSS caps display height at 32rem, which is not a substitute for resizing the file. Two files (`assets/img/20250501/gas.jpg`, `20250504/clean.jpg`) are AVIF misnamed `.jpg` — browsers cope, Python imaging libraries cannot.

### Publication covers

600×400 in `assets/images/covers/`. Papers use a figure from the paper; presentations and talks with slides use the deck's title page; everything else has none. **Always the whole figure, contain-fit with white padding — never a crop.** A centre-crop cuts subfigure labels, legends, and scale bars; every paper cover carried that defect until they were re-rendered. The canvas size is only for consistent row heights, since the template renders covers with no `object-fit`. `assets/images/empty_300x200.png` is the lazy-load placeholder and is referenced only from a Liquid template — a `_site`-only grep will not see it, so do not "clean it up".

### External scripts

Every external script and stylesheet carries an `integrity` hash and a pinned version. Adding one without SRI, or reverting to a floating version like `masonry-layout@4`, undoes that. A wrong hash blocks the script silently, so verify in a browser after touching them.

## Old URLs that must keep working

These were live on the pre-migration site and are preserved by `redirect_from` / `redirect_to`. Breaking them breaks inbound links from Google Scholar, ORCID, and CVs:

`/Research/` → `/publications/` · `/gallery/` and `/Gallery/` → `/showcase/` · `/archive/` → `/blog/` · `/cv/` → the CV PDF · plus a `redirect_from` on every news item moved out of `_posts/`.

## Branches

- **`master`** — published. Pushing here goes live.
- **`prototype`** — working branch.
- **`backup-original-site`** — the pre-migration site at `da1b6df`, local and on origin. Do not touch; it holds the only copies of 13 retired gallery images and the original full-size photos.

GitHub Pages has occasionally not picked up a push. If no build appears, request one:

```bash
gh api -X POST repos/Erin-1919/Erin-1919.github.io/pages/builds
gh api repos/Erin-1919/Erin-1919.github.io/pages/builds/latest --jq '{status, commit: .commit[0:7]}'
```

## Skills

`.claude/skills/` (gitignored, local only) holds two repo-specific skills:

- **`erin-blog-post`** — writing a post or news item, including which collection it belongs in and Erin's style rules.
- **`research-item`** — adding a publication, presentation, talk, or thesis, and keeping the CV `.docx`/`.pdf` in sync via `add_cv_entry.py`.

Under-review work appears in the CV but **is not listed on the website**.

## Documentation

`docs/superpowers/` holds the design spec and implementation plan for the theme migration, kept for reference on why things are structured this way.
