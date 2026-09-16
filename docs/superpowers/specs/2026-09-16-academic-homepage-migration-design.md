# Migrating to the academic-homepage theme

Date: 2026-09-16
Branch: `prototype`
Backup: `backup-original-site` at `da1b6df` (pushed to origin)

## Goal

Replace the current custom Jekyll theme with
[luost26/academic-homepage](https://github.com/luost26/academic-homepage), adopting the
theme's content model rather than merely restyling the existing pages. The site is
re-framed around Erin Li's new position: Assistant Professor, University of Guelph.

## Why this theme

- Jekyll 3.9 with one whitelisted plugin (`jekyll-email-protect`), so it builds on classic
  GitHub Pages. No Actions workflow needed, unlike al-folio or Chirpy.
- Publications are YAML front matter, not BibTeX. The existing `research.md` entries port
  by hand-editing rather than by conversion.
- Ships a news feed, which matches how Erin already writes about conferences and talks.
- Blog is first-class, so `_posts/` carries over.

## Decisions

| Question | Decision |
|---|---|
| Migration scope | Adopt the theme's model fully, not a visual refresh |
| Event posts | Move to `_news/`; extend the theme so news items have bodies |
| Publications page | Keep the four-tab interface (Publications / Presentations / Talks / Thesis) |
| Publication covers | Selected papers only; the rest use the no-cover variant |
| Gallery | Showcase collection + lightbox; posters only, highlights unpublished |
| Home Layout 2 | Removed |
| Honors & Awards | Omitted — student-era awards do not fit the faculty framing |
| Past postdoc | Shown in an Experience block below Education |
| Social links | LinkedIn, Google Scholar, GitHub |

## Target structure

```
_data/          profile.yml, navigation.yml, display.yml, authors.yml
_publications/  ~20 entries, `category:` drives the tabs
_news/          ~20 event entries moved from _posts/, with bodies
_posts/         ~42 technical and reading posts, unchanged
_showcase/      3 poster cards
_layouts/       theme's, plus news.html
_includes/      theme's widgets, with news_card and publication_item modified
publications.html, news.html, blog.html, showcase.html, index.html
assets/         existing img and pdf trees, plus the theme's css and js
```

Removed: `_sass/`, the old `_includes/`, `blog.md`, `research.md`, `gallery.md`,
`cv.html`, `archive.html`, `index_layout2.html`.

The CV becomes a navbar link to the PDF via `cv_link` in `profile.yml`, replacing the
embedded-viewer page.

Navigation: Home, Publications, News, Blog, Showcase, CV. News earns its own page because
roughly 20 entries will not fit the home feed, which shows the latest 5.

## Content mapping

### Home

| Block | Source |
|---|---|
| Portrait, name, position | `assets/img/Erin_Li_34.jpg`; Assistant Professor, University of Guelph |
| Social | LinkedIn, Google Scholar, GitHub |
| About Me | New prose bio. The current home page is a fact list, not prose. |
| Education | PhD, University of Calgary (2023); M.Sc., University of New Brunswick (2019); undergraduate degree supplied by Erin |
| Experience | Postdoctoral scholar, University of Calgary |
| News | Latest 5, linking to full entries |
| Selected Publications | ~5 papers marked `selected: true`, with covers |

### Publications

Each entry becomes `_publications/<year>/<slug>.md` carrying `category`
(`paper` / `presentation` / `talk` / `thesis`), `pub`, `pub_date`, `authors`, `links`, and
the existing full abstract.

The theme's `abstract` field is designed as a one-to-two sentence inline summary. Erin's
abstracts are full paragraphs, so `widgets/publication_item.html` gains a collapsible
toggle that preserves the current `<details>` behaviour.

Author bolding moves from inline `**Li, M.**` markup to the theme's `authors` list plus
`_data/authors.yml`.

### News

The ~20 conference, talk, and award posts move from `_posts/` to `_news/` with their text
and photos intact. Each carries `redirect_from` with its old permalink so existing links
resolve.

### Blog

The remaining ~42 posts stay in `_posts/` unchanged.

### Showcase

Three poster cards, each linking to its PDF, with GLightbox for click-to-enlarge. The 13
highlight images remain in `assets/` but are not published; Erin is deciding whether to
retire them.

## Theme modifications

Four changes to upstream, kept isolated so what is custom stays visible:

1. `_layouts/news.html` and a `news.html` index page, giving news items real pages.
   `widgets/news_card.html` is modified so titles link to them.
2. `publications.html` renders four tabs over `category`, styled to the theme.
3. `widgets/publication_item.html` gains the collapsible abstract.
4. `showcase.html` wires in GLightbox (~10 KB, CDN).

Config: clear `baseurl`, add `jekyll-redirect-from` and `jekyll-paginate`, retain the
existing site metadata from `_config.yml`.

## Jekyll version

The current Gemfile pins Jekyll 4.2 while GitHub Pages classic builds with 3.9, so local
builds diverge from production today. Moving to 3.9 to match the theme also closes that
gap.

## Implementation sequence

Incremental, with a checkpoint commit per layer so any layer can be reviewed or reverted
on its own.

1. Theme skeleton, config, and `profile.yml`; home page renders.
2. Publications collection and the four-tab page.
3. News: layout, index, moved posts, redirects.
4. Blog: remaining posts verified under the new layouts.
5. Showcase and lightbox.
6. CV link, navigation, and a full link and asset audit.

Each step ends with a clean `bundle exec jekyll build` and a local visual check of the
layer just migrated. The final step verifies every internal link and PDF path resolves,
which is where migrations of this kind usually rot.

## Inputs required from Erin

Implementation blocks on these where noted:

- Google Scholar ID and the public email address for the new position — needed at step 1.
- Whether ResearchGate stays alongside the three chosen social links — needed at step 1.
- Undergraduate institution, degree, and dates — needed at step 1.
- Which ~5 papers are `selected`, and a cover image for each — needed at step 2.
- Review of the drafted bio prose — drafted at step 1, revised any time after.

## Out of scope

- Updating the CV PDF itself to reflect the Guelph position.
- Retiring or re-curating the 13 highlight images.
- Merging `prototype` into `master`, which is a separate decision once the site is
  reviewed.
