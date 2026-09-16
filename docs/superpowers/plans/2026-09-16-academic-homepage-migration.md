# Academic Homepage Migration Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Replace the custom Jekyll theme on `Erin-1919.github.io` with luost26/academic-homepage, migrating all existing content into the theme's collection model and re-framing the site around Erin Li's new position as Assistant Professor at the University of Guelph.

**Architecture:** The theme's file tree is grafted onto the existing repository on the `prototype` branch. Content moves into four collections — `_publications`, `_news`, `_posts`, `_showcase` — and the theme receives four targeted modifications (news bodies, publication tabs, collapsible abstracts, lightbox). Existing `assets/` trees are preserved untouched. Work proceeds one layer at a time with a checkpoint commit per layer.

**Tech Stack:** Jekyll 3.9, Ruby 3.4.4, Bundler 2.6.9, Liquid, Bootstrap 4 (bundled by theme), GLightbox 3.x (CDN), `jekyll-email-protect`, `jekyll-redirect-from`, `jekyll-paginate`.

**Spec:** `docs/superpowers/specs/2026-09-16-academic-homepage-migration-design.md`

## Global Constraints

- Branch is `prototype`. Never commit to `master` during this plan.
- Backup branch `backup-original-site` at `da1b6df` must remain untouched.
- Jekyll is pinned to `~> 3.9` to match GitHub Pages classic build. Do not upgrade to 4.x.
- Ruby 3.4 removed `csv`, `base64`, and `logger` from stdlib. All three must be explicit gems or Jekyll 3.9 will not boot.
- Only GitHub Pages whitelisted plugins may be used: `jekyll-email-protect`, `jekyll-redirect-from`, `jekyll-paginate`. No others.
- `baseurl` must be empty. The theme ships `baseurl: "/academic-homepage"`, which breaks every asset path on a user site.
- Everything under `assets/img/` and `assets/pdf/` is existing content. Never delete or rename files in those trees.
- Site metadata (`title`, `author`, `description`, `lang`) is carried over verbatim from the current `_config.yml`.
- Erin's name renders as `Mingke (Erin) Li` in author lists and must be bolded via `_data/authors.yml`.
- Every commit message ends with the trailer `Co-Authored-By: Claude Opus 5 (1M context) <noreply@anthropic.com>`.

**Verification model.** This is a static site with no unit test framework. A "test" in this plan means: run the build, then assert on the generated HTML in `_site/` with `grep`. Every task follows write-assertion → run and watch it fail → implement → run and watch it pass → commit. Build command throughout:

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && bundle exec jekyll build 2>&1 | tail -20
```

A build that prints `done in N seconds` with no `Error:` or `Liquid Warning:` lines is a passing build.

---

### Task 1: Toolchain and theme skeleton

Brings the theme's scaffolding into the repo and gets a clean build with the site's own metadata. The home page will still show placeholder profile content at the end of this task; Task 2 replaces it.

**Files:**
- Create: `Gemfile` (replace existing), `_config.yml` (replace existing)
- Create: `_layouts/default.html`, `_layouts/blog_post.html`, `_layouts/prompt.html`
- Create: `_includes/footer.html`, `_includes/navbar.html`, `_includes/widgets/*.html`
- Create: `_data/authors.yml`, `_data/display.yml`, `_data/navigation.yml`, `_data/profile.yml`
- Create: `index.html` (replace existing), `blog.html`, `publications.html`, `showcase.html`, `404.html` (replace existing)
- Create: `assets/css/`, `assets/js/`, `assets/images/` from the theme
- Delete: `_sass/`, `_includes/archive.html`, `_includes/embed.html`, `_includes/gallery.html`, `_includes/home.html`, `_includes/menu.html`, `_includes/meta.html`, `_includes/sidebar.html`, `_layouts/page.html`, `_layouts/post.html`, `archive.html`, `cv.html`, `blog.md`, `research.md`, `gallery.md`, `index_layout2.html`
- Source: the theme clone at `C:/Users/mlier/AppData/Local/Temp/claude/E--UCalgary-postdoc-Erin-1919-github-io/ccb0259c-998b-4a87-90dd-09b3b4ac176a/scratchpad/theme`

**Interfaces:**
- Consumes: nothing.
- Produces: a building Jekyll 3.9 site with collections `publications`, `news`, `showcase`, `posts` declared; `site.data.profile`, `site.data.display`, `site.data.navigation`, `site.data.authors` available to all later tasks; `_includes/widgets/publication_item.html`, `_includes/widgets/news_card.html`, `_includes/widgets/blog_card.html` present and unmodified, ready for Tasks 3 and 4 to edit.

- [ ] **Step 1: Confirm the branch and clean tree**

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && git branch --show-current && git status --short
```

Expected: prints `prototype` and no uncommitted changes. If the branch is not `prototype`, stop — do not proceed on another branch.

- [ ] **Step 2: Write the failing assertion**

The site must build and the generated home page must carry the theme's profile card markup. Assert it now, before anything is installed:

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && bundle exec jekyll build 2>&1 | tail -5 && grep -c "profile-card\|navbar" _site/index.html
```

- [ ] **Step 3: Run it to verify it fails**

Expected: the build fails, or `_site/index.html` contains no theme markup (grep returns `0` or errors with "No such file"). Either outcome is the expected failure.

- [ ] **Step 4: Copy the theme scaffolding in**

Copy theme files, deliberately excluding the theme's sample content and its git metadata:

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io
THEME="C:/Users/mlier/AppData/Local/Temp/claude/E--UCalgary-postdoc-Erin-1919-github-io/ccb0259c-998b-4a87-90dd-09b3b4ac176a/scratchpad/theme"
rm -rf _sass _layouts _includes
cp -r "$THEME/_layouts" "$THEME/_includes" "$THEME/_data" .
cp "$THEME/index.html" "$THEME/blog.html" "$THEME/publications.html" "$THEME/showcase.html" "$THEME/404.html" .
cp -r "$THEME/assets/css" "$THEME/assets/js" assets/
mkdir -p assets/images && cp -r "$THEME/assets/images/." assets/images/
git rm -q --cached -r _sass 2>/dev/null; true
rm -f blog.md research.md gallery.md cv.html archive.html index_layout2.html
```

Note: `index_layout2.html` is never copied, so the removal is a safety net only.

- [ ] **Step 5: Write the Gemfile**

Replace `Gemfile` entirely. The three stdlib gems are mandatory on Ruby 3.4:

```ruby
source "https://rubygems.org"

gem "jekyll", "~> 3.9"

# Ruby 3.4 removed these from stdlib; Jekyll 3.9 will not boot without them.
gem "csv"
gem "base64"
gem "logger"

group :jekyll_plugins do
  gem "jekyll-email-protect"
  gem "jekyll-redirect-from"
  gem "jekyll-paginate"
end

gem "tzinfo-data", platforms: [:mingw, :mswin, :x64_mingw, :jruby]
gem "wdm", "~> 0.2" if Gem.win_platform?
gem "webrick", "~> 1.7"
gem "kramdown-parser-gfm"
```

- [ ] **Step 6: Write `_config.yml`**

Replace it entirely. Site metadata is carried over from the old config; `baseurl` is empty:

```yaml
title: "Mingke Erin Li"
author: "Mingke Erin Li"
description: "Bring Your Own Bottle & Do Your Own Research."
lang: "en"
baseurl: ""
url: "https://Erin-1919.github.io"

markdown: kramdown
kramdown:
  input: GFM

plugins:
  - jekyll-email-protect
  - jekyll-redirect-from
  - jekyll-paginate

collections:
  - publications
  - news
  - showcase
  - posts

defaults:
  - scope:
      path: ""
      type: "posts"
    values:
      layout: "blog_post"

exclude:
  - Gemfile
  - Gemfile.lock
  - vendor/
  - docs/
  - CLAUDE.md
  - UNLICENSE.txt
```

- [ ] **Step 7: Delete the theme's sample content**

The theme's `_publications`, `_news`, `_showcase`, and `_posts` samples must not ship. They were never copied in Step 4, but confirm none exist:

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && ls _publications _news _showcase 2>&1 | head -5
```

Expected: "No such file or directory" for all three. They are created with real content in Tasks 3, 4, and 6.

- [ ] **Step 8: Install and run the assertion**

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && bundle install 2>&1 | tail -5 && bundle exec jekyll build 2>&1 | tail -10
```

Expected: `bundle install` completes, then the build prints `done in N seconds` with no `Error:` line.

If the build fails with `cannot load such file -- csv` (or `base64`/`logger`), the Gemfile in Step 5 was not applied — re-check it. If it fails with a Liquid error naming `site.data.profile`, that is expected only if `_data/profile.yml` failed to copy; re-run Step 4.

- [ ] **Step 9: Verify the home page carries theme markup**

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && grep -c "navbar" _site/index.html && grep -o "academic-homepage" _site/index.html | head -1
```

Expected: a non-zero count for `navbar`. The theme's footer credit link is expected to appear and is kept.

- [ ] **Step 10: Commit**

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && git add -A && git commit -m "$(cat <<'EOF'
Replace custom theme with academic-homepage scaffolding

Swap Jekyll 4.2 for 3.9 to match the GitHub Pages classic builder, and
add the Ruby 3.4 stdlib gems Jekyll 3.9 needs to boot.

Co-Authored-By: Claude Opus 5 (1M context) <noreply@anthropic.com>
EOF
)"
```

---

### Task 2: Profile, navigation, and home page

Replaces the theme's placeholder cat-themed profile with Erin's real identity.

All inputs have been collected — this task is no longer blocked. For the record: Scholar ID `F3F4-2sAAAAJ`; email `mli.erin1919@gmail.com`; ResearchGate kept as a fourth icon; education and work history taken from `assets/pdf/cv/Mingke_Li_CV_2026.pdf`; appointment is Assistant Professor, Department of Geography, Environment & Geomatics, College of Social and Applied Human Sciences, University of Guelph.

The appointment start date was not supplied and is not used — the theme's `positions:` block renders name lines without dates.

**Files:**
- Modify: `_data/profile.yml` (full rewrite)
- Modify: `_data/navigation.yml` (full rewrite)
- Modify: `_data/display.yml`
- Modify: `_data/authors.yml`
- Modify: `index.html:12-18` (remove debug widgets)

**Interfaces:**
- Consumes: the building site from Task 1.
- Produces: `site.data.profile.education`, `site.data.profile.experience`, `site.data.profile.cv_link`; `_data/authors.yml` with the key `Mingke (Erin) Li` marked `me: true`, which `widgets/author_list.html` uses to bold her name in every publication entry in Task 3.

- [ ] **Step 1: Write the failing assertion**

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && grep -q "Assistant Professor" _site/index.html && grep -q "University of Guelph" _site/index.html && echo PASS || echo FAIL
```

- [ ] **Step 2: Run it to verify it fails**

Expected: `FAIL`. The home page still shows "Title or Position" and "Affiliation Name".

- [ ] **Step 3: Write `_data/profile.yml`**

Every value below is final — all inputs have been collected. Write the file exactly as given.

```yaml
primary_name: "Mingke (Erin) Li"
secondary_name: ""
navbar_name: "Mingke (Erin) Li"

positions:
- name: Assistant Professor
- name: Department of Geography, Environment & Geomatics
- name: College of Social and Applied Human Sciences, University of Guelph

email: "mli.erin1919@gmail.com"
cv_link: /assets/pdf/cv/Mingke_Li_CV_2026.pdf
gscholar: F3F4-2sAAAAJ
github: Erin-1919
linkedin: mingke-erin-li
researchgate: Mingke-Li

short_bio_text_justify: false
short_bio: >-
  <p>
    I am an Assistant Professor in the Department of Geography, Environment &amp; Geomatics at the <a href="https://www.uoguelph.ca/" target="_blank">University of Guelph</a>,
    working at the intersection of geospatial data science, GeoAI, and Digital Earth. My research centres on
    Discrete Global Grid Systems (DGGS) as a spatial framework for integrating and analysing heterogeneous
    Earth observation data across scales.
  </p>
  <p>
    My work spans multi-resolution terrain and hydrological modelling, methane and greenhouse gas inventories
    on equal-area discrete global grids, and agentic multi-LLM systems for spatial reasoning. I contribute to
    the Open Geospatial Consortium's DGGS and EmissionML working groups. I hold a Ph.D. in Geomatics
    Engineering from the University of Calgary, where I was previously a postdoctoral associate.
  </p>

portrait_url: /assets/img/Erin_Li_34.jpg

education:
- name: University of Calgary
  position: >-
    Department of Geomatics Engineering <br/>
    Ph.D. in Geomatics Engineering
  date: 2023
- name: University of New Brunswick
  position: M.Sc. in Forestry
  date: 2019
- name: Nanjing Forestry University
  position: B.Sc. in Geographic Information Science
  date: 2017

experience:
- name: University of Calgary
  position: Postdoctoral Associate
  date: 2024 - 2026
- name: Geosapiens Inc.
  position: Geospatial Scientist
  date: 2023 - 2024
- name: University of Calgary
  position: >-
    Department of Geomatics Engineering <br/>
    Sessional Instructor
  date: 2020 - 2023

# Awards are omitted from the homepage while the site is framed around the
# faculty position. Restore by setting show_awards: true in _data/display.yml.
# awards:
# - name: Esri Young Scholar Award, First Runner-Up
#   date: 2022
# - name: Esri ECCE App Challenge, First Runner-Up
#   date: 2021
```

The bio above is a draft written from the repository's own evidence. Erin reviews and revises it; treat her wording as final over this text.

- [ ] **Step 4: Write `_data/navigation.yml`**

```yaml
pages:
- name: Home
  url: /
- name: Publications
  url: /publications
- name: News
  url: /news
- name: Blog
  url: /blog
- name: Showcase
  url: /showcase
```

The CV is reached through the profile card's `cv_link`, not the navbar, which is how the theme is designed.

- [ ] **Step 5: Write `_data/display.yml`**

```yaml
homepage:
  show_experience: true
  show_news: true
  show_selected_publications: true
  num_news: 5

footer_text: >-
  <a href="https://github.com/luost26/academic-homepage" target="_blank"><i class="fas fa-pencil-ruler"></i> academic-homepage</a>
```

- [ ] **Step 6: Write `_data/authors.yml`**

```yaml
"Li, M.":
  name: "Li, M."
  bold: true

"Mingke (Erin) Li":
  bold: true
```

The theme's `widgets/author_list.html` bolds an author when their entry has `bold: true` — not `me: true`. Both spellings are listed because migrated entries in Task 3 use the citation form `Li, M.` while the profile uses the full name.

Two conventions the widget supports, worth knowing when writing entries in Task 3: an author name suffixed `*` renders an equal-contribution mark, and `#` renders a corresponding-author mark, both with an automatic footnote. Co-authors may also be given `url:` keys here to link their homepages.

- [ ] **Step 7: Remove the debug widgets from `index.html`**

Delete these three lines from `index.html`:

```html
        <!-- Debugging widgets -->
        {% include widgets/debug_repo_name.html %}
        {% include widgets/debug_url.html %}
```

- [ ] **Step 7b: Add a ResearchGate branch to both profile cards**

The theme supports Google Scholar, GitHub, Twitter, LinkedIn, and ORCID, but not ResearchGate. Erin keeps ResearchGate, so both cards need a fifth branch.

In `_includes/widgets/profile_card_mini.html`, immediately after the `linkedin` block's `{% endif %}`, insert:

```html
                        {% if site.data.profile.researchgate %}
                        <a class="px-1 no-break" target="_blank" href="https://www.researchgate.net/profile/{{ site.data.profile.researchgate }}">
                            <i class="fab fa-researchgate"></i>
                        </a>
                        {% endif %}
```

In `_includes/widgets/profile_card.html`, in the same position, insert the labelled variant matching that file's style:

```html
                        {% if site.data.profile.researchgate %}
                        <a class="pr-3 no-break" target="_blank" href="https://www.researchgate.net/profile/{{ site.data.profile.researchgate }}">
                            <i class="fab fa-researchgate"></i> ResearchGate
                        </a>
                        {% endif %}
```

`fa-researchgate` ships in Font Awesome's brands set, which the theme already loads, so no new dependency.

- [ ] **Step 8: Rebuild and run the assertion**

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && bundle exec jekyll build 2>&1 | tail -5 && grep -q "Assistant Professor" _site/index.html && grep -q "University of Guelph" _site/index.html && echo PASS || echo FAIL
```

Expected: `PASS`.

- [ ] **Step 9: Verify the portrait and Twitter removal**

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && grep -o "Erin_Li_34.jpg" _site/index.html | head -1 && grep -c "twitter" _site/index.html
```

Expected: the portrait filename appears; the twitter count is `0`. If twitter markup persists, the `twitter:` key was left in `profile.yml` — remove it.

- [ ] **Step 10: Commit**

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && git add -A && git commit -m "$(cat <<'EOF'
Set profile to Assistant Professor at University of Guelph

Replace the theme's placeholder identity with real bio, education, and
experience. Drop the awards block and Twitter link.

Co-Authored-By: Claude Opus 5 (1M context) <noreply@anthropic.com>
EOF
)"
```

---

### Task 3: Publications collection and four-tab page

Migrates the ~20 entries in the old `research.md` into `_publications/`, adds the tab interface, and makes abstracts collapsible.

**BLOCKED ON INPUT (partial).** Steps 1–9 proceed without Erin. Step 10 needs her list of ~5 papers to mark `selected: true` and a cover image for each. If the list is not yet available, complete Steps 1–9, commit, and hold Step 10.

**Files:**
- Create: `_publications/<year>/<slug>.md` — one per entry, ~20 files
- Modify: `publications.html` (full rewrite)
- Modify: `_includes/widgets/publication_item.html` (collapsible abstract)
- Source content: `git show da1b6df:research.md`

**Interfaces:**
- Consumes: `_data/authors.yml` from Task 2 for author bolding.
- Produces: every document in `site.publications` carries `category` with exactly one of `paper`, `presentation`, `talk`, `thesis`; `selected: true` on ~5 of them, which `index.html` already filters on.

- [ ] **Step 1: Write the failing assertion**

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && grep -q 'id="tab-presentation"' _site/publications/index.html && grep -q "QuadGridSIM" _site/publications/index.html && echo PASS || echo FAIL
```

- [ ] **Step 2: Run it to verify it fails**

Expected: `FAIL` — `_publications/` does not exist yet, so the page renders empty.

- [ ] **Step 3: Recover the source content**

The old research page was deleted in Task 1. Recover it for reference:

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && git show da1b6df:research.md > /c/Users/mlier/AppData/Local/Temp/claude/E--UCalgary-postdoc-Erin-1919-github-io/ccb0259c-998b-4a87-90dd-09b3b4ac176a/scratchpad/research-source.md && wc -l < /c/Users/mlier/AppData/Local/Temp/claude/E--UCalgary-postdoc-Erin-1919-github-io/ccb0259c-998b-4a87-90dd-09b3b4ac176a/scratchpad/research-source.md
```

Expected: `267`.

- [ ] **Step 4: Create one publication file per entry**

One file per entry at `_publications/<year>/<year>-<lastname>-<shortslug>.md`. This is the exact shape, using a real entry as the worked example:

```yaml
---
title:          "QuadGridSIM: A quadrilateral grid-based method for high-performance and robust trajectory similarity analysis"
date:           2024-01-01
selected:       false
category:       paper
pub:            "Transactions in GIS"
pub_date:       "2024"
pub_post:       ", 28(1), 83–107."
abstract: >-
  Measuring trajectory similarity is a fundamental algorithm in trajectory data mining, playing a key role in
  trajectory clustering, pattern mining, and classification, for instance. However, existing trajectory
  similarity measures based on vector representation have challenges in achieving both fast and accurate
  similarity measurements. [...full abstract text carried over verbatim from research.md...]
authors:
- Liu, J.
- Li, J.
- Qiao, L.
- Li, M.
- Stefanakis, E.
- Zhao, X.
- Huang, Q.
- Wang, H.
- Zhang, C.
links:
  DOI: https://doi.org/10.1111/tgis.13126
  PDF: /assets/pdf/papers/2024_TransGIS_Liu_QuadGridSIM_published.pdf
---
```

Rules that apply to every file:

- `category` is `paper` for the Publications tab, `presentation` for Conference Presentations, `talk` for Other Invited Talks, `thesis` for the two theses. Take the category from which `<div class="tab-content">` block the entry sat in.
- `date` is `<year>-01-01` unless a more precise date is known. It only drives sort order within a year.
- `authors` entries drop the markdown bolding; `Li, M.` is bolded automatically by `_data/authors.yml`.
- `abstract` is the full text from inside the entry's `<details>` block, carried over verbatim. Do not summarise or truncate.
- PDF links change from the absolute `https://Erin-1919.github.io/assets/pdf/...` form to site-relative `/assets/pdf/...`. The files themselves do not move.
- Entries with no abstract in the source simply omit the `abstract` key.
- `selected` is `false` on every file at this step; Step 10 flips ~5 of them.

`research.md` is the complete and authoritative source for this task. Migrate exactly what is in it — add nothing, drop nothing.

This was verified rather than assumed: every publication title in `assets/pdf/cv/Mingke_Li_CV_2026.pdf` was diffed against `research.md`. The only CV entries absent from `research.md` are items still under review (IJGIS, Scientific Data, JOSS, Computers and Geosciences). Erin's ruling: **under-review work is not listed publicly**, so those are correctly excluded and no file is created for them.

Note for author lists: `research.md` uses two citation forms for Erin — the older `Li, M.` and the newer `Li, M.E.`. Both must appear in `_data/authors.yml` with `bold: true` (Task 2 writes that file) or the newer entries will not bold her name. Use whichever form the source entry uses; do not normalise them.

- [ ] **Step 5: Verify the file count and category spread**

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && find _publications -name '*.md' | wc -l && grep -rh "^category:" _publications | sort | uniq -c
```

Expected: a total matching the number of entries in `research-source.md`, and four category values present with `thesis` appearing exactly twice.

- [ ] **Step 6: Add the collapsible abstract to `publication_item.html`**

The widget renders the abstract twice — once in the desktop block, once in the mobile block. Replace **both** occurrences of this line:

```html
            <p class="mt-0 mb-0 small text-muted">{{ item.abstract }}</p>
```

with:

```html
            {%- if item.abstract -%}
            <details class="mt-0 mb-0 small text-muted pub-abstract">
                <summary>Abstract</summary>
                {{ item.abstract }}
            </details>
            {%- endif -%}
```

- [ ] **Step 7: Rewrite `publications.html` with tabs**

```html
---
layout: default
title : Publications
navbar_title: Publications
---

{% assign tabs = "paper,presentation,talk,thesis" | split: "," %}
{% assign labels = "Publications,Conference Presentations,Invited Talks,Thesis" | split: "," %}

<div class="row">
    <div class="col-12">
        <ul class="nav nav-pills pt-4 mb-3" id="pub-tabs" role="tablist">
            {% for t in tabs %}
            <li class="nav-item">
                <a class="nav-link {% if forloop.first %}active{% endif %}" id="pill-{{ t }}"
                   data-toggle="pill" href="#tab-{{ t }}" role="tab" aria-controls="tab-{{ t }}"
                   aria-selected="{% if forloop.first %}true{% else %}false{% endif %}">
                    {{ labels[forloop.index0] }}
                </a>
            </li>
            {% endfor %}
        </ul>

        <div class="tab-content" id="pub-tab-content">
            {% for t in tabs %}
            <div class="tab-pane fade {% if forloop.first %}show active{% endif %}"
                 id="tab-{{ t }}" role="tabpanel" aria-labelledby="pill-{{ t }}">
                {% assign items = site.publications | where: "category", t | sort: "date" | reverse %}
                {% assign by_year = items | group_by_exp: "item", "item.date | date: '%Y'" %}
                {% for year in by_year %}
                <h2 class="pt-3" id="{{ t }}-year-{{ year.name }}">{{ year.name }}</h2>
                <div class="my-0 p-0 bg-white shadow-sm rounded-xl">
                    {% for item in year.items %}
                        {% include widgets/publication_item.html item=item hide_bottom_border=forloop.last first=forloop.first last=forloop.last %}
                    {% endfor %}
                </div>
                {% endfor %}
            </div>
            {% endfor %}
        </div>
    </div>
</div>
```

This uses Bootstrap 4's pill-tab component, which the theme already bundles — no new JS dependency and no hand-rolled `showTab()` function. The year sidebar from the original page is dropped because it cannot track four independent tab panes.

- [ ] **Step 8: Rebuild and run the assertion**

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && bundle exec jekyll build 2>&1 | tail -5 && grep -q 'id="tab-presentation"' _site/publications/index.html && grep -q "QuadGridSIM" _site/publications/index.html && echo PASS || echo FAIL
```

Expected: `PASS`.

- [ ] **Step 9: Verify author bolding and PDF paths**

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && grep -c "font-weight-bold\|<strong>" _site/publications/index.html && grep -o 'href="/assets/pdf/papers/[^"]*"' _site/publications/index.html | wc -l && grep -c "Erin-1919.github.io/assets" _site/publications/index.html
```

Expected: a non-zero bold count, a PDF link count matching the entries that have PDFs, and `0` absolute `Erin-1919.github.io/assets` links remaining.

- [ ] **Step 10: Mark selected publications and add covers**

Erin's chosen five, with covers already generated from each paper's own PDF and committed at 600×400:

| File | cover |
|---|---|
| `_publications/2026/2026-li-gridmind.md` | `/assets/images/covers/cover_gridmind.jpg` |
| `_publications/2026/2026-li-methane-digital-earth.md` | `/assets/images/covers/cover_methane.jpg` |
| `_publications/2024/2024-li-serverless-visualization.md` | `/assets/images/covers/cover_serverless.jpg` |
| `_publications/2022/2022-li-multiresolution-topographic.md` | `/assets/images/covers/cover_topographic.jpg` |
| `_publications/2020/2020-li-geospatial-operations-comparison.md` | `/assets/images/covers/cover_operations.jpg` |

Every other entry keeps `selected: false` and no `cover` key — the theme renders a generated visual hash for them, which is a deliberate design feature, not a missing image.

Verify:

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && bundle exec jekyll build 2>&1 | tail -3 && grep -c "Selected Publications" _site/index.html && grep -rc "^selected:       true" _publications | grep -v ":0" | wc -l
```

Expected: `Selected Publications` appears on the home page, and the count of files with `selected: true` matches Erin's list length.

- [ ] **Step 11: Commit**

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && git add -A && git commit -m "$(cat <<'EOF'
Migrate research.md into the publications collection

Split the four-tab research page into per-entry files carrying a category,
rebuild the page on Bootstrap pill tabs, and make abstracts collapsible.

Co-Authored-By: Claude Opus 5 (1M context) <noreply@anthropic.com>
EOF
)"
```

---

### Task 4: News collection with bodies

Extends the theme so news items are real pages, then moves the event posts across with redirects.

**BLOCKED ON INPUT (partial).** Steps 1–6 proceed without Erin. Step 7 needs her ruling on four ambiguous posts, listed there.

**Files:**
- Create: `_layouts/news.html`
- Create: `news.html`
- Modify: `_includes/widgets/news_card.html:14-16`
- Modify: `_config.yml` (add the `news` defaults block)
- Move: ~18 files from `_posts/` to `_news/`

**Interfaces:**
- Consumes: the `news` collection declared in Task 1.
- Produces: `site.news` documents. Those with a body render at `/news/<slug>/` and are linked; those without a body render as plain headline text and are never linked. Moved posts carry `redirect_from` with their former permalink.

**Two shapes of news item.** Erin writes news both ways and both must work:

1. **With a body** — the migrated conference and award posts, each 170–950 words plus a photo. These get a full page and their headline links to it.
2. **Title only** — a one-line announcement with no body, the way the theme ships. These render as plain text with a date and are NOT clickable, because an empty page behind a link is a dead end.

Every template that renders a news item must branch on this. The test for "has a body" is the rendered content stripped of HTML and whitespace:

```liquid
{%- assign body = item.content | strip_html | strip -%}
{%- if body != "" -%} ... linked ... {%- else -%} ... plain ... {%- endif -%}
```

Use exactly this test everywhere, so the two templates never disagree about which items are clickable.

- [ ] **Step 1: Write the failing assertion**

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && test -f _site/news/index.html && grep -q "ISPRS" _site/news/index.html && echo PASS || echo FAIL
```

- [ ] **Step 2: Run it to verify it fails**

Expected: `FAIL` — no news index exists.

- [ ] **Step 3: Make the news collection output pages**

Add to `_config.yml`, replacing the bare `collections:` list from Task 1:

```yaml
collections:
  publications:
    output: false
  news:
    output: true
    permalink: /news/:path/
  showcase:
    output: false
  posts:
    output: true
```

`publications` and `showcase` stay `output: false` because they are rendered entirely by their index pages and need no standalone URLs.

Then add to the `defaults:` block:

```yaml
  - scope:
      path: ""
      type: "news"
    values:
      layout: "news"
```

- [ ] **Step 4: Create `_layouts/news.html`**

```html
---
layout: default
---

<div class="row">
    <div class="col-12 col-lg-10 mx-auto">
        <div class="my-3 p-4 bg-white shadow-sm rounded-xl">
            <h2 class="mt-0 mb-2">{{ page.title }}</h2>
            <div class="text-muted small mb-4">
                <i class="fas fa-calendar-alt"></i> {{ page.date | date: "%B %d, %Y" }}
            </div>
            <div class="news-content">
                {{ content }}
            </div>
            <div class="mt-4 pt-3 border-top border-gray">
                <a href="{{ '/news' | relative_url }}"><i class="fas fa-angle-double-left"></i> All news</a>
            </div>
        </div>
    </div>
</div>
```

- [ ] **Step 5: Create `news.html`**

```html
---
layout: default
title : News
navbar_title: News
---

{% assign news_by_year = site.news | sort: "date" | reverse | group_by_exp: "item", "item.date | date: '%Y'" %}

<div class="row">
    <div class="col-12 col-lg-10">
        {% for year in news_by_year %}
        <h2 class="pt-4" id="year-{{ year.name }}">{{ year.name }}</h2>
        <div class="my-0 p-0 bg-white shadow-sm rounded-xl">
            {% for item in year.items %}
            {%- assign body = item.content | strip_html | strip -%}
            <div class="border-bottom border-gray p-3 {% if forloop.last %}border-0{% endif %}">
                <h5 class="mb-2">
                    {%- if body != "" -%}
                    <a href="{{ item.url | relative_url }}" class="text-dark text-decoration-none">{{ item.title }}</a>
                    {%- else -%}
                    {{ item.title }}
                    {%- endif -%}
                </h5>
                <div class="text-muted small mb-2">
                    <i class="fas fa-calendar-alt"></i> {{ item.date | date: "%B %d, %Y" }}
                </div>
                {%- if body != "" -%}
                <div class="text-muted small">{{ body | truncate: 300 }}</div>
                {%- endif -%}
            </div>
            {% endfor %}
        </div>
        {% endfor %}
    </div>

    <div class="col-2 d-none d-lg-block">
        <div id="navbar-year" class="nav nav-pills flex-column sticky-top" style="top: 80px">
            {% for year in news_by_year %}
            <a class="nav-link d-block" href="#year-{{ year.name }}">{{ year.name }}</a>
            {% endfor %}
        </div>
    </div>
</div>
```

- [ ] **Step 6: Make home-page news headlines link to their pages**

In `_includes/widgets/news_card.html`, replace this line:

```html
                    <div>{{ item.title }}</div>
```

with the branching version, so only items that have a body become links:

```html
                    {%- assign body = item.content | strip_html | strip -%}
                    <div>
                        {%- if body != "" -%}
                        <a href="{{ item.url | relative_url }}" class="text-dark">{{ item.title }}</a>
                        {%- else -%}
                        {{ item.title }}
                        {%- endif -%}
                    </div>
```

Then add an "All news" link. Replace the closing of the widget's header line:

```html
    <h6 class="p-3 mb-0 border-bottom border-gray"><i class="fas fa-rss"></i> News</h6>
```

with:

```html
    <h6 class="p-3 mb-0 border-bottom border-gray d-flex">
        <span><i class="fas fa-rss"></i> News</span>
        <a class="ml-auto small" href="{{ '/news' | relative_url }}">All news <i class="fas fa-angle-double-right"></i></a>
    </h6>
```

- [ ] **Step 7: Move the event posts**

These 18 move from `_posts/` to `_news/`:

```
2019-03-15-A-Poster-on-Master's-Projects.md
2019-08-26-Master-Thesis.md
2020-11-18-AutoCarto-Conference-2020.md
2021-01-12-Doggone-Candidacy-Exam.md
2021-05-03-Geomatics-Engineering-Research-Department-News.md
2021-05-19-Esri-ECCE-App-Challenge-First-Runner-Up.md
2021-05-26-Canadian-Cartographic-Association-Conference-2021.md
2022-01-10-ISPRS-Webinar.md
2022-04-27-Esri-Young-Scholar-Award-First-Runner-Up.md
2022-05-25-Canadian-Cartographic Association-Conference-2022.md
2023-03-03-GIS-Education-Research-Conference.md
2023-06-02-Video-Feature-on-Geomatics-Engineering.md
2024-11-06-130th-OGC-meeting-methane.md
2025-05-08-CanCH4-Symposium-Ottawa.md
2025-06-11-OGC132-DGGS-EmissionML.md
2025-10-31-innovation-summit-nl-digital-earth.md
2026-01-26-ogc-dggs-ai-panel.md
2026-07-09-DGGS-Spatial-Harness-for-AI-ISPRS-Congress.md
```

Four more are genuinely ambiguous and need Erin's ruling before moving — they read as external writing or media rather than events she attended:

```
2019-02-28-Geoprocessing-Scripts-Using-Python-Esri-Course.md
2019-03-03-Esri-ECCE-Blog-Customized-Script-Tool-in-ArcGIS.md
2020-04-02-Esri-ECCE-Blog-R-ArcGIS-Bridge.md
2022-03-25-Flood-Susceptibility-Modeling-on-Hexagonal Grid Meshes.md
```

Ask her which belong in News. Do not move them on a guess — a wrong move is silent and only surfaces when she notices a post missing from the blog.

Move with `git mv` so history follows the file:

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && mkdir -p _news && git mv "_posts/2022-01-10-ISPRS-Webinar.md" "_news/2022-01-10-ISPRS-Webinar.md"
```

Repeat for each file in the confirmed list.

- [ ] **Step 8: Add redirects to every moved file**

The old permalink was `/:title/` — the title slug alone, no date. For each moved file, add `redirect_from` to its front matter. Worked example for `_news/2022-01-10-ISPRS-Webinar.md`:

```yaml
---
title: "ISPRS Webinar"
layout: news
date: 2022-01-10
redirect_from:
  - /ISPRS-Webinar/
---
```

The redirect path is the old post's title slug, which is the filename with the date prefix and `.md` stripped. Preserve each file's existing `title:` exactly.

**Replace** the existing `layout: post` line — do not add a second `layout:` key. Every moved file already carries `layout: post` from the old theme, and a duplicate key is a hard YAML error that fails the build. Add `date:` and `redirect_from:` as new keys.

Verify no file ended up with two layout keys before building:

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && for f in _news/*.md; do n=$(awk '/^---$/{c++} c==1 && /^layout:/{print}' "$f" | wc -l); [ "$n" -gt 1 ] && echo "DUPLICATE $f"; done; echo "checked"
```

Expected: no `DUPLICATE` lines.

- [ ] **Step 9: Rebuild and run the assertion**

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && bundle exec jekyll build 2>&1 | tail -5 && test -f _site/news/index.html && grep -q "ISPRS" _site/news/index.html && echo PASS || echo FAIL
```

Expected: `PASS`.

- [ ] **Step 10: Verify redirects and body preservation**

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && test -f "_site/ISPRS-Webinar/index.html" && grep -q "refresh" "_site/ISPRS-Webinar/index.html" && echo "REDIRECT OK" ; find _site/news -name index.html | wc -l ; grep -c "<img" _site/news/2022-01-10-ISPRS-Webinar/index.html
```

Expected: `REDIRECT OK`; a news page count equal to the number of moved files (the `/news` index is written to `_site/news/index.html`, not into this tree, so it is not counted here); and a non-zero image count proving bodies and photos survived.

- [ ] **Step 10b: Verify both news shapes render correctly**

Every migrated item has a body, so the title-only branch is untested by the migration alone. Create one real title-only item to exercise it — this is a genuine entry, not a placeholder:

`_news/2026-09-16-guelph-appointment.md`

```yaml
---
title: "Joined the University of Guelph as an Assistant Professor in the Department of Geography, Environment & Geomatics."
date: 2026-09-16
---
```

Then confirm the two shapes behave differently:

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && bundle exec jekyll build 2>&1 | tail -3
echo "--- title-only item must NOT be a link on the index ---"
grep -A3 'Joined the University of Guelph' _site/news/index.html | grep -c '<a href' 
echo "--- an item WITH a body must be a link ---"
grep -B2 -A3 'ISPRS' _site/news/index.html | grep -c '<a href'
```

Expected: `0` for the title-only item and a non-zero count for the item with a body. If the title-only item renders as a link, the `body != ""` branch is wrong and would produce a link to an empty page.

- [ ] **Step 11: Commit**

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && git add -A && git commit -m "$(cat <<'EOF'
Add news collection with full pages and move event posts into it

Extend the theme with a news layout and index so news items carry bodies,
and redirect each moved post's old permalink.

Co-Authored-By: Claude Opus 5 (1M context) <noreply@anthropic.com>
EOF
)"
```

---

### Task 5: Blog verification

The remaining posts need no content changes, but their front matter references layouts that no longer exist.

**Files:**
- Modify: front matter of any post still naming `layout: post`
- Verify: `blog.html` from Task 1

**Interfaces:**
- Consumes: the `blog_post` layout default set in Task 1's `_config.yml`.
- Produces: every remaining post rendering under `blog_post`.

- [ ] **Step 1: Write the failing assertion**

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && grep -rl "^layout: post$" _posts | wc -l
```

Expected at the end of this task: `0`.

- [ ] **Step 2: Run it to see the current count**

Expected: a non-zero count — most posts declare `layout: post`, which Task 1 deleted.

- [ ] **Step 3: Strip the stale layout declarations**

The `defaults:` block in `_config.yml` already assigns `blog_post` to every post, so the per-file declaration is redundant and wrong:

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && sed -i '/^layout: post$/d' _posts/*.md && grep -rl "^layout: post$" _posts | wc -l
```

Expected: `0`.

- [ ] **Step 4: Rebuild and verify every post rendered**

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && bundle exec jekyll build 2>&1 | tail -5 && ls _posts/*.md | wc -l && grep -c "blog_card\|Read more" _site/blog/index.html
```

Expected: a clean build, and the blog index listing a "Read more" per remaining post.

- [ ] **Step 5: Check for math-bearing posts**

The old theme loaded KaTeX from the local `assets/katex/` bundle, gated on `mathjax: true` front matter. **The new theme already loads KaTeX 0.16.11 from jsDelivr with SRI on every page**, in both `_layouts/default.html` and `_layouts/blog_post.html`. No hook is needed and none should be added — injecting a second copy would double-load the library.

Verify math still renders on a post that uses it:

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && grep -rl "^mathjax: true" _posts | head -3 && grep -c "katex" _site/blog/index.html
```

Expected: a non-zero `katex` count, confirming the theme's KaTeX tags reach rendered pages. If any post is listed, open it in the local server during Task 7 Step 7 and confirm its formulae render.

Leave `assets/katex/` in place. It is now unreferenced, and it is triaged alongside the `_data/font-awesome/` orphan in Task 7 — not deleted here.

- [ ] **Step 5b: Move the one remaining post Erin ruled is news**

Task 4 left four ambiguous posts in `_posts/` pending her decision. Her ruling: **only the Esri Python course post moves.** The two Esri ECCE blog posts and the flood-susceptibility post stay in the blog.

Move it exactly as Task 4 moved the others — `git mv`, replace `layout: post` with `layout: news`, add `date:` and `redirect_from:`:

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && git mv "_posts/2019-02-28-Geoprocessing-Scripts-Using-Python-Esri-Course.md" "_news/2019-02-28-Geoprocessing-Scripts-Using-Python-Esri-Course.md"
```

Its front matter becomes:

```yaml
---
title: "<keep the file's existing title verbatim>"
date: 2019-02-28
redirect_from:
  - /Geoprocessing-Scripts-Using-Python-Esri-Course/
---
```

Verify the redirect resolves: `_site/Geoprocessing-Scripts-Using-Python-Esri-Course/index.html` must exist and contain a refresh redirect.

- [ ] **Step 5c: Rename the two remaining filenames containing spaces**

Two posts still carry a literal space in their filename. A space already broke one redirect in Task 4; remove the trap:

```
_posts/2018-07-01-Spatial-Patterns-of-Spruce-Budworm-Defoliation-and-Tree-Mortality-A Review.md
_posts/2022-03-25-Flood-Susceptibility-Modeling-on-Hexagonal Grid Meshes.md
```

Rename each space to a hyphen with `git mv`. **This is URL-neutral and must stay that way:** Jekyll's `:title` permalink slugifies the space to a hyphen already, so the published URL is identical before and after. Task 4 proved this — the live site serves the hyphenated form for a file whose name contained a space.

Prove the URLs did not move:

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && bundle exec jekyll build 2>&1 | tail -3
test -d "_site/Spatial-Patterns-of-Spruce-Budworm-Defoliation-and-Tree-Mortality-A-Review" && echo "OK sbw" || echo "URL MOVED - investigate"
test -d "_site/Flood-Susceptibility-Modeling-on-Hexagonal-Grid-Meshes" && echo "OK flood" || echo "URL MOVED - investigate"
find _site -name "* *" -not -path "_site/assets/img/*" | head
```

Expected: both `OK` lines, and the `find` returning nothing outside `assets/img/` (one pre-existing image there legitimately has a space in its name and is off-limits).

If either prints `URL MOVED`, the rename changed the published URL — revert that file with `git mv` back and report it, because a silently moved post URL breaks inbound links.

- [ ] **Step 6: Commit**

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && git commit _posts _news _layouts -m "$(cat <<'EOF'
Point remaining blog posts at the new layout

Drop the per-post layout declaration now that the config default assigns
blog_post, and keep KaTeX loading for math posts.

Co-Authored-By: Claude Opus 5 (1M context) <noreply@anthropic.com>
EOF
)"
```

---

### Task 6: Showcase and lightbox

Three poster cards with click-to-enlarge. The 13 highlight images stay on disk, unpublished.

**Files:**
- Create: `_showcase/posters/canch4-2025.md`, `_showcase/posters/esri-2022.md`, `_showcase/posters/esri-2019.md`
- Modify: `showcase.html`

**Interfaces:**
- Consumes: the `showcase` collection from Task 1.
- Produces: three documents with `show: true`, `group: Posters`, `width: 4`.

- [ ] **Step 1: Write the failing assertion**

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && grep -q "glightbox" _site/showcase/index.html && grep -c "CanCH4" _site/showcase/index.html && echo PASS || echo FAIL
```

- [ ] **Step 2: Run it to verify it fails**

Expected: `FAIL`.

- [ ] **Step 3: Create the three poster cards**

`_showcase/posters/canch4-2025.md`:

```markdown
---
show: true
width: 4
date: 2025-05-01
group: Posters
---

<a href="/assets/img/academic/posters/1CanCH4_poster_Li_2025.jpg" class="glightbox" data-gallery="posters"
   data-description="CanCH4 Symposium, 2025">
  <img src="/assets/img/academic/posters/1CanCH4_poster_Li_2025.jpg" class="w-100 rounded-sm" alt="CanCH4 poster, 2025">
</a>
<div class="p-3">
  <h6 class="mb-1">CanCH4 Symposium</h6>
  <p class="small text-muted mb-1">2025</p>
  <a class="small" href="/assets/pdf/posters/CanCH4_Poster_May_2025_EL.pdf" target="_blank">[PDF]</a>
</div>
```

`_showcase/posters/esri-2022.md`:

```markdown
---
show: true
width: 4
date: 2022-05-01
group: Posters
---

<a href="/assets/img/academic/posters/2ESRI_poster_Li_2022.jpg" class="glightbox" data-gallery="posters"
   data-description="Esri Young Scholar, 2022">
  <img src="/assets/img/academic/posters/2ESRI_poster_Li_2022.jpg" class="w-100 rounded-sm" alt="Esri poster, 2022">
</a>
<div class="p-3">
  <h6 class="mb-1">Esri Young Scholar</h6>
  <p class="small text-muted mb-1">2022</p>
  <a class="small" href="/assets/pdf/posters/ESRI_poster_Li_2022.pdf" target="_blank">[PDF]</a>
</div>
```

`_showcase/posters/esri-2019.md`:

```markdown
---
show: true
width: 4
date: 2019-05-01
group: Posters
---

<a href="/assets/img/academic/posters/3ESRI_poster_Li_2019.jpg" class="glightbox" data-gallery="posters"
   data-description="Esri Canada GIS Scholarship, 2019">
  <img src="/assets/img/academic/posters/3ESRI_poster_Li_2019.jpg" class="w-100 rounded-sm" alt="Esri poster, 2019">
</a>
<div class="p-3">
  <h6 class="mb-1">Esri Canada GIS Scholarship</h6>
  <p class="small text-muted mb-1">2019</p>
  <a class="small" href="/assets/pdf/posters/ESRI_poster_Li_2019.pdf" target="_blank">[PDF]</a>
</div>
```

Confirm the three PDF filenames against `assets/pdf/posters/` before writing — they come from the old `gallery.md` front matter and must resolve.

- [ ] **Step 4: Wire GLightbox into `showcase.html`**

Append to the end of `showcase.html`:

```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/glightbox@3.3.1/dist/css/glightbox.min.css"
      integrity="<sha384 hash generated below>" crossorigin="anonymous">
<script src="https://cdn.jsdelivr.net/npm/glightbox@3.3.1/dist/js/glightbox.min.js"
        integrity="<sha384 hash generated below>" crossorigin="anonymous"></script>
<script>
  GLightbox({ selector: '.glightbox', touchNavigation: true, loop: true });
</script>
```

Subresource Integrity is required on both tags. Without it, a compromised CDN can serve arbitrary JavaScript into the site. Generate the two hashes first:

```bash
cd /c/Users/mlier/AppData/Local/Temp/claude/E--UCalgary-postdoc-Erin-1919-github-io/ccb0259c-998b-4a87-90dd-09b3b4ac176a/scratchpad \
  && curl -sL -o gl.css https://cdn.jsdelivr.net/npm/glightbox@3.3.1/dist/css/glightbox.min.css \
  && curl -sL -o gl.js  https://cdn.jsdelivr.net/npm/glightbox@3.3.1/dist/js/glightbox.min.js \
  && echo "css sha384-$(openssl dgst -sha384 -binary gl.css | openssl base64 -A)" \
  && echo "js  sha384-$(openssl dgst -sha384 -binary gl.js  | openssl base64 -A)"
```

Paste each `sha384-...` value into the matching tag. If `openssl` is unavailable, take the hashes from the jsDelivr web UI, which publishes an SRI snippet per file.

If Erin would rather not depend on a CDN at all, vendor both files into `assets/js/` and `assets/css/` and reference them with `relative_url` — the integrity attributes then become unnecessary. That is a one-line change to this step; ask her preference at Task 6 rather than assuming.

- [ ] **Step 5: Rebuild and run the assertion**

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && bundle exec jekyll build 2>&1 | tail -5 && grep -q "glightbox" _site/showcase/index.html && grep -q "CanCH4" _site/showcase/index.html && echo PASS || echo FAIL
```

Expected: `PASS`.

- [ ] **Step 6: Verify the poster images and PDFs resolve**

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && for p in $(grep -o '/assets/[^"]*\.\(jpg\|pdf\)' _site/showcase/index.html | sort -u); do test -f "_site$p" && echo "OK $p" || echo "MISSING $p"; done
```

Expected: every line reads `OK`. Any `MISSING` means a filename mismatch — fix before committing.

- [ ] **Step 7: Commit**

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && git add -A && git commit -m "$(cat <<'EOF'
Add poster showcase with lightbox

Three poster cards linking to their PDFs. Highlight images stay on disk,
unpublished, pending a decision on retiring them.

Co-Authored-By: Claude Opus 5 (1M context) <noreply@anthropic.com>
EOF
)"
```

---

### Task 7: Site-wide audit

The step that catches what a page-by-page migration misses.

**Files:**
- Modify: whatever the audit turns up

**Interfaces:**
- Consumes: the complete site from Tasks 1–6.
- Produces: a site with no broken internal links, no stale absolute URLs, and no orphaned references.

- [ ] **Step 1: Write the failing assertion**

Every internal link and asset reference in the built site must resolve to a file:

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && grep -rhoE '(href|src)="/[^"]*"' _site --include=*.html | sed -E 's/^(href|src)="//; s/"$//' | grep -v '^//' | sed 's/#.*//' | sort -u > /c/Users/mlier/AppData/Local/Temp/claude/E--UCalgary-postdoc-Erin-1919-github-io/ccb0259c-998b-4a87-90dd-09b3b4ac176a/scratchpad/links.txt && MISSING=0; while read -r p; do [ -z "$p" ] && continue; if [ ! -e "_site$p" ] && [ ! -e "_site$p/index.html" ] && [ ! -e "_site${p%/}.html" ]; then echo "MISSING $p"; MISSING=1; fi; done < /c/Users/mlier/AppData/Local/Temp/claude/E--UCalgary-postdoc-Erin-1919-github-io/ccb0259c-998b-4a87-90dd-09b3b4ac176a/scratchpad/links.txt; echo "exit=$MISSING"
```

- [ ] **Step 2: Run it and collect the failures**

Expected: some `MISSING` lines. Common causes, in the order they usually appear: references to the deleted `cv.html`, `research.md`, or `gallery.md` from inside post bodies; theme sample images under `/assets/images/` that were never copied; and absolute `https://Erin-1919.github.io/assets/...` links inside old post bodies that the grep above does not catch.

- [ ] **Step 3: Fix each missing reference**

For links to deleted pages, repoint them: `/Research/` becomes `/publications`, gallery links become `/showcase`, CV links become `/assets/pdf/cv/Mingke_Li_CV_2026.pdf`. For missing theme sample images, copy them from the theme clone's `assets/images/` or remove the reference if it belongs to deleted sample content.

- [ ] **Step 4: Normalise absolute self-links in post bodies**

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && grep -rl "https://Erin-1919.github.io/assets" _posts _news | wc -l
```

If non-zero, rewrite them to site-relative so the site works on a local server and under any future domain:

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && sed -i 's|https://Erin-1919\.github\.io/assets|/assets|g' _posts/*.md _news/*.md && grep -rc "Erin-1919.github.io/assets" _posts _news | grep -v ":0" | wc -l
```

Expected: `0`.

- [ ] **Step 5: Rebuild and re-run the link audit**

Re-run the Step 1 command.

Expected: no `MISSING` lines and `exit=0`.

- [ ] **Step 6: Verify navigation reaches every section**

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && for n in index publications news blog showcase; do if [ -f "_site/$n.html" ] || [ -f "_site/$n/index.html" ]; then echo "OK /$n"; else echo "MISSING /$n"; fi; done && grep -o 'href="[^"]*Mingke_Li_CV[^"]*"' _site/index.html | head -1
```

Expected: every nav target `OK`, and the CV PDF link present on the home page.

- [ ] **Step 6b: Sweep unused theme assets**

The theme shipped sample content — cat photos, MIT/PKU badge logos, placeholder covers, README screenshots — plus the old theme left orphans behind. Remove what nothing references.

**Scope, strictly.** Sweep ONLY these theme-provided paths:

```
assets/images/   assets/css/   assets/js/   assets/fonts/
assets/fontawesome/   assets/katex/   _data/font-awesome/
```

**NEVER sweep `assets/img/` or `assets/pdf/`.** They hold Erin's own content. Some of it is deliberately unpublished — the 13 gallery highlight images are unreferenced on purpose, pending her decision — so "unreferenced" there does NOT mean "unused". Leave both trees completely alone.

**`assets/images/empty_300x200.png` must be KEPT.** It is the lazy-load placeholder in `widgets/publication_item.html` and is referenced from a Liquid template, not from static HTML. Deleting it breaks every coverless publication entry.

Build first, then compute what the rendered site actually references:

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && bundle exec jekyll build 2>&1 | tail -3
SP=/c/Users/mlier/AppData/Local/Temp/claude/E--UCalgary-postdoc-Erin-1919-github-io/ccb0259c-998b-4a87-90dd-09b3b4ac176a/scratchpad
grep -rhoE '/assets/[A-Za-z0-9._/-]+' _site --include=*.html --include=*.css --include=*.js \
  | sed 's|^/||' | sort -u > "$SP/referenced.txt"
grep -rhoE '/assets/[A-Za-z0-9._/-]+' _layouts _includes *.html _data 2>/dev/null \
  | sed 's|^/||' | sort -u >> "$SP/referenced.txt"
sort -u "$SP/referenced.txt" -o "$SP/referenced.txt"
for d in assets/images assets/css assets/js assets/fonts assets/fontawesome assets/katex; do
  [ -d "$d" ] || continue
  find "$d" -type f | while read -r f; do
    grep -qxF "$f" "$SP/referenced.txt" || echo "UNREFERENCED $f"
  done
done
```

Review the `UNREFERENCED` list before deleting anything. Expected on it: `assets/images/etc/*` (cat photos, beaver, preview), `assets/images/photos/portrait.jpg` (the theme's placeholder portrait), `assets/images/badges/*` (MIT and PKU logos — Erin's education entries carry no `logo:` key), `assets/images/covers/cover1.jpg`, `cover2.jpg`, `cover3.jpg` (theme samples), `assets/images/variants/*` (README screenshots), and all of `assets/katex/` (the theme loads KaTeX from a CDN instead).

If `empty_300x200.png` appears on the list, the second grep above failed to read the templates — stop and fix the command rather than deleting it.

Delete with `git rm`, then prove the site is unharmed:

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && git rm -r -q --ignore-unmatch \
  assets/images/etc assets/images/photos assets/images/badges assets/images/variants \
  assets/images/covers/cover1.jpg assets/images/covers/cover2.jpg assets/images/covers/cover3.jpg \
  assets/katex _data/font-awesome
bundle exec jekyll build 2>&1 | grep -E "Error|done in" | tail -3
test -f assets/images/empty_300x200.png && echo "placeholder KEPT" || echo "PLACEHOLDER LOST - RESTORE IT"
```

Then re-run Step 1's link audit. It must still report no `MISSING` lines — that is the proof the sweep removed nothing load-bearing. If any appear, restore the named file with `git checkout HEAD -- <path>` and leave it in place.

`assets/fonts/` and `assets/fontawesome/` are old-theme leftovers. Include them in the sweep only if the audit shows nothing references them; the theme bundles its own Font Awesome, so it likely does not.

- [ ] **Step 7: Serve and review visually**

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && bundle exec jekyll serve --port 4000
```

Open `http://localhost:4000` and check each page at desktop and phone widths: home profile card and news feed, publications tabs switching, a news item's body and photo, the blog listing, and the poster lightbox opening.

- [ ] **Step 8: Commit**

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && git add -A && git commit -m "$(cat <<'EOF'
Fix broken links and normalise asset paths after migration

Repoint references to removed pages and convert absolute self-links in
post bodies to site-relative.

Co-Authored-By: Claude Opus 5 (1M context) <noreply@anthropic.com>
EOF
)"
```

---

## Not in this plan

- Merging `prototype` into `master`. The site goes live the moment master moves, so that is Erin's call after she reviews the branch.
- Updating the CV PDF to reflect the Guelph position.
- Retiring the 13 highlight images.
- Any redirect for the old `/Research/`, `/Gallery/`, or CV page URLs beyond repointing internal links. Add `redirect_from` to the new pages if external sites link to the old ones.

---

### Task 8: Rolling news window on the home page

Runs after Task 6, before Task 7's audit. The home page currently shows a fixed count of news items regardless of age, so a quiet period leaves years-old entries under a heading called "News". Replace the fixed count with a rolling time window.

**Files:**
- Modify: `_includes/widgets/news_card.html`
- Modify: `_data/display.yml`
- Modify: `index.html` (the include's parameters)

**Interfaces:**
- Consumes: `site.news` from Task 4; the "All news" header link already added in Task 4.
- Produces: a home-page news block showing only items inside the window, with a minimum floor so it is never empty.

**Behaviour:** show every news item dated within the last 12 months. If fewer than `min_news` items fall inside that window, show the most recent `min_news` instead, so the block never renders empty during a quiet stretch. The full list stays one click away via the existing "All news" link.

- [ ] **Step 1: Write the failing assertion**

With today's content, three items fall inside a 12-month window (Guelph appointment, ISPRS Congress, Innovation Summit NL) and nothing from 2024 or earlier should appear on the home page. Note the Jan 2026 OGC DGGS AI panel entry was reclassified as a blog post and is no longer news, so it must not be used as an in-window example:

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && bundle exec jekyll build 2>&1 | tail -3 && grep -c "130th OGC\|CanCH4 Symposium" _site/index.html
```

- [ ] **Step 2: Run it to verify it fails**

Expected: a non-zero count — 2024/2025 items are currently on the home page because the widget takes a fixed slice by count, not by date.

- [ ] **Step 3: Add the window to `_data/display.yml`**

Replace the `num_news` key:

```yaml
homepage:
  show_experience: true
  show_news: true
  show_selected_publications: true
  news_months: 12
  min_news: 3
```

- [ ] **Step 4: Pass the new parameters in `index.html`**

Replace the news include line:

```html
        {% include widgets/news_card.html months=site.data.display.homepage.news_months min=site.data.display.homepage.min_news %}
```

- [ ] **Step 5: Compute the window in `news_card.html`**

Replace the widget's first line (the `assign news_by_year = ...` line) with:

```liquid
{%- assign sorted = site.news | sort: "date" | reverse -%}
{%- assign window_seconds = include.months | times: 2629746 -%}
{%- assign cutoff = site.time | date: "%s" | plus: 0 | minus: window_seconds -%}
{%- assign n = 0 -%}
{%- for item in sorted -%}
  {%- assign ts = item.date | date: "%s" | plus: 0 -%}
  {%- if ts >= cutoff -%}{%- assign n = n | plus: 1 -%}{%- endif -%}
{%- endfor -%}
{%- if n < include.min -%}{%- assign n = include.min -%}{%- endif -%}
{%- assign news_by_year = sorted | slice: 0, n | group_by_exp: "item", "item.date | date: '%Y'" -%}
```

This works because `sorted` is in descending date order, so every item inside the window is a prefix of the list — counting them and taking `slice: 0, n` is equivalent to filtering, without needing an array-append filter that Jekyll's Liquid does not provide. `2629746` is the average seconds per month.

Leave the rest of the widget untouched, including the two-shape linked/unlinked branch from Task 4 and the "All news" header link.

- [ ] **Step 6: Rebuild and run the assertion**

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && bundle exec jekyll build 2>&1 | tail -3
echo "--- 2024-and-older items must be absent from the home page ---"
grep -c "130th OGC\|CanCH4 Symposium\|GIS Education" _site/index.html
echo "--- recent items must be present ---"
grep -c "Guelph\|ISPRS Congress" _site/index.html
echo "--- full list still reachable ---"
grep -c "All news" _site/index.html
```

Expected: `0` for the old items, non-zero for the recent ones, and `1` for the "All news" link.

- [ ] **Step 7: Prove the floor works**

The floor only triggers when the window is nearly empty, which today's content does not exercise. Test it by temporarily setting `news_months: 1` in `_data/display.yml`, rebuilding, and confirming the home page still lists `min_news` items rather than none:

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && sed -i 's/news_months: 12/news_months: 1/' _data/display.yml && bundle exec jekyll build 2>&1 | tail -2 && grep -c "fas fa-rss" _site/index.html && grep -o 'news/[a-z0-9-]*/' _site/index.html | sort -u | wc -l
```

Expected: the News block is still present and lists at least `min_news` entries. **Then restore `news_months: 12`** and rebuild before committing — do not leave the test value in place.

- [ ] **Step 8: Commit**

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && git commit _includes/widgets/news_card.html _data/display.yml index.html -m "$(cat <<'EOF'
Show only the last 12 months of news on the home page

Fall back to the most recent few items when the window is empty, so the
block never renders blank. The full list stays behind the All news link.

Co-Authored-By: Claude Opus 5 (1M context) <noreply@anthropic.com>
EOF
)"
```

---

### Task 9: News curation and the incoming-appointment correction

Runs after Task 6, before Task 8. Applies the site owner's review of the news list, and corrects a factual overstatement about her current position.

**Files:**
- Modify: `_data/profile.yml`
- Modify: `_news/2026-09-16-guelph-appointment.md` (renamed)
- Move: 4 files from `_news/` to `_posts/`

**Interfaces:**
- Consumes: the news collection from Task 4 and the profile from Task 2.
- Produces: `_news/` containing only 2020-and-later items; a profile that states the appointment accurately.

**The correction that matters most.** Erin signed her Guelph offer on 2026-07-23 but does not start until December 2026. The site currently asserts she IS an Assistant Professor there, which is not true yet. Her decision: use the standard academic convention, **"Incoming Assistant Professor"**, and keep her current UCalgary role visible.

- [ ] **Step 1: Write the failing assertion**

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && bundle exec jekyll build 2>&1 | tail -3
echo "--- profile must say Incoming ---"; grep -c "Incoming Assistant Professor" _site/index.html
echo "--- no news before 2020 ---"; grep -c "Master Thesis\|A Poster on Master\|Doggone" _site/news/index.html
```

- [ ] **Step 2: Run it to verify it fails**

Expected: `0` for the Incoming check and a non-zero count for the pre-2020 items.

- [ ] **Step 3: Correct the position in `_data/profile.yml`**

Replace the `positions:` block with:

```yaml
positions:
- name: Incoming Assistant Professor
- name: Department of Geography, Environment & Geomatics
- name: University of Guelph (from December 2026)
```

The `experience:` block already lists `Postdoctoral Associate, University of Calgary, 2024 - 2026`, so her current role stays visible. Leave `education:` and `experience:` untouched.

- [ ] **Step 4: Correct the bio's opening sentence**

In the same file, the `short_bio` currently opens by asserting the Guelph role in the present tense. Replace only that opening clause so it reads:

```html
    I am a postdoctoral associate at the University of Calgary and an incoming Assistant Professor in the
    Department of Geography, Environment &amp; Geomatics at the
    <a href="https://www.uoguelph.ca/" target="_blank">University of Guelph</a>, starting December 2026.
    My work sits at the intersection of geospatial data science, GeoAI, and Digital Earth, centred on
    Discrete Global Grid Systems (DGGS) as a spatial framework for integrating and analysing heterogeneous
    Earth observation data across scales.
```

Leave the bio's second paragraph exactly as it is.

- [ ] **Step 5: Re-date and reword the appointment news item**

The entry is dated 2026-09-16 and worded as though she has joined. The real date is the offer signing, 2026-07-23.

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && git mv _news/2026-09-16-guelph-appointment.md _news/2026-07-23-guelph-appointment.md
```

Its front matter becomes, with no body (it stays a title-only item):

```yaml
---
title: "Signed an offer to join the University of Guelph as an Assistant Professor in the Department of Geography, Environment & Geomatics, starting December 2026."
date: 2026-07-23
---
```

- [ ] **Step 6: Move four items out of news, back to posts**

Erin's ruling: **no news before 2020**, and the candidacy-exam post belongs in the blog. These four move back to `_posts/`:

```
_news/2019-02-28-Geoprocessing-Scripts-Using-Python-Esri-Course.md
_news/2019-03-15-A-Poster-on-Master's-Projects.md
_news/2019-08-26-Master-Thesis.md
_news/2021-01-12-Doggone-Candidacy-Exam.md
```

Note the first was moved INTO news earlier in this migration; the "no news before 2020" ruling supersedes that. For each file, `git mv` it to `_posts/` and then **remove both the `redirect_from:` key and the `layout:` key**. Back in `_posts/` the file's own published URL is exactly what `redirect_from` pointed at, so leaving the key makes Jekyll emit a redirect stub at the same path as the post — the post would redirect to itself. The `_config.yml` defaults block supplies `layout: blog_post`, so no explicit layout is wanted. Keep `title:` and `date:`.

- [ ] **Step 7: Rebuild and run the assertions**

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && rm -rf _site && bundle exec jekyll build 2>&1 | tail -3
echo "--- Incoming present ---"; grep -c "Incoming Assistant Professor" _site/index.html
echo "--- pre-2020 news gone ---"; grep -c "Master Thesis\|A Poster on Master\|Doggone" _site/news/index.html
echo "--- the 4 are real posts, not redirect stubs ---"
for s in Geoprocessing-Scripts-Using-Python-Esri-Course "A-Poster-on-Master's-Projects" Master-Thesis Doggone-Candidacy-Exam; do
  if [ -f "_site/$s/index.html" ]; then
    if grep -q refresh "_site/$s/index.html"; then echo "STUB (BAD) /$s"; else echo "OK /$s"; fi
  else echo "MISSING /$s"; fi
done
echo "--- counts ---"; echo "_posts: $(ls _posts/*.md | wc -l)  _news: $(ls _news/*.md | wc -l)"
echo "--- earliest news ---"; grep -h "^date:" _news/*.md | sort | head -1
```

Expected: `1` for Incoming; `0` for the pre-2020 items; four `OK` lines with no `STUB` or `MISSING`; `_posts` = 48 and `_news` = 15; and the earliest news date in 2020 or later.

- [ ] **Step 8: Commit**

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && git commit _data/profile.yml _news _posts -m "$(cat <<'EOF'
Present the Guelph role as incoming and curate news to 2020 onward

The appointment starts December 2026, so the profile no longer asserts
it in the present tense. Four pre-2020 and personal-milestone entries
move back to the blog.

Co-Authored-By: Claude Opus 5 (1M context) <noreply@anthropic.com>
EOF
)"
```

---

### Task 10: Home-page card fixes and uniform publication covers

Fixes three rendering defects the site owner found while reviewing the built site, and makes publication covers consistent.

**Files:**
- Modify: `_includes/widgets/experience_card.html`
- Modify: `_includes/widgets/publication_card.html`
- Modify: `_includes/widgets/publication_item.html`
- Modify: 25 files under `_publications/` (add a `cover:` key)

**Interfaces:**
- Consumes: the cover images committed at `assets/images/covers/` (30 files: 5 curated figures, 10 `paper_*.jpg`, 15 `slide_*.jpg`).
- Produces: an Education/Experience block with no broken images, a single "All publications" link, and publication entries that either show a real cover or show no image at all.

- [ ] **Step 1: Write the failing assertions**

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && bundle exec jekyll build -d _site_t10 2>&1 | tail -3
echo "--- broken logo imgs on home (expect >0 now, 0 after) ---"; grep -c 'img src="" ' _site_t10/index.html
echo "--- duplicate all-publications links (expect 2 now, 1 after) ---"; grep -c "publications\">" _site_t10/index.html
echo "--- generated bubble-hash placeholders (expect >0 now, 0 after) ---"; grep -c "bubble-visual-hash" _site_t10/publications/index.html
```

- [ ] **Step 2: Run them and record the actual counts**

- [ ] **Step 3: Only render an institution logo when one exists**

In `_includes/widgets/experience_card.html` there are TWO identical `<img>` lines — one in the Education loop, one in the Experience loop. Neither entry type in this site sets `logo:`, so both render `src=""`, producing a broken-image icon whose 18px-wide `alt` text wraps one character per line. That is the vertical letter-stacking on the home page.

Replace **both** occurrences of:

```html
                                    <img src="{{ item.logo | relative_url }}" alt="{{ item.name }}" style="width: 18px;" class="mr-1 mt-1">
```

with:

```html
                                    {%- if item.logo -%}
                                    <img src="{{ item.logo | relative_url }}" alt="{{ item.name }}" style="width: 18px;" class="mr-1 mt-1">
                                    {%- endif -%}
```

Do not add logo images. The owner has not supplied any and inventing institutional logos is not wanted.

- [ ] **Step 4: Keep one "All publications" link, matching the news card**

`_includes/widgets/publication_card.html` currently renders the link twice: `(view all »)` in the header and `All publications »` in a footer. Replace the whole widget's header and drop the footer, so it matches `news_card.html`'s pattern exactly:

```html
{% assign publications = include.publications %}
<div class="my-3 p-0 bg-white shadow-sm rounded-xl">
    <h6 class="border-bottom border-gray p-3 mb-0 d-flex">
        <span>{% if include.title %}{{ include.title }}{% else %}<i class="fas fa-star"></i> Selected Recent Publications{% endif %}</span>
        <a class="ml-auto small no-break" href="{{ '/publications' | relative_url }}">All publications <i class="fas fa-angle-double-right"></i></a>
    </h6>
    {% for item in publications limit:include.limit %}
        {% include widgets/publication_item.html item=item first=false last=false %}
    {% endfor %}
</div>
```

- [ ] **Step 5: Show no image at all when an entry has no cover**

`_includes/widgets/publication_item.html` falls back to a generated `bubble-visual-hash` SVG whenever `cover:` is absent. The owner wants no placeholder: entries without a cover should show text only.

In the **desktop block**, replace the whole cover column:

```html
        <div class="col-md-3 col-xl-2 mb-md-0 p-md-3">
            {%- if item.cover -%}
            <img data-src="{{ item.cover | relative_url }}" alt="{{ item.title }}" class="lazy w-100 rounded-sm" src="{{ '/assets/images/empty_300x200.png' | relative_url }}">
            {%- else -%}
            <svg class="bubble-visual-hash lazy w-100 rounded-sm" data-bubble-visual-hash="{{ item.id }}" viewBox="0 0 300 200"></svg>
            {%- endif -%}
        </div>
```

with a version that omits the column entirely when there is no cover, letting the text span the full width:

```html
        {%- if item.cover -%}
        <div class="col-md-3 col-xl-2 mb-md-0 p-md-3">
            <img data-src="{{ item.cover | relative_url }}" alt="{{ item.title }}" class="lazy w-100 rounded-sm" src="{{ '/assets/images/empty_300x200.png' | relative_url }}">
        </div>
        {%- endif -%}
```

The text column immediately after it is `<div class="col-md-9 col-xl-10 p-3 pl-md-0">`. Make its width conditional so it fills the row when there is no cover:

```html
        <div class="{% if item.cover %}col-md-9 col-xl-10 p-3 pl-md-0{% else %}col-12 p-3{% endif %}">
```

In the **mobile block** lower in the same file, the cover is used as a background image via `data-src` on the outer row div; that already degrades correctly when `item.cover` is empty, so leave the mobile block alone apart from confirming it renders no broken image.

`assets/images/empty_300x200.png` is still required as the lazy-load placeholder — do not remove it.

- [ ] **Step 6: Add the `cover:` key to 25 publication entries**

The exact file-to-cover mapping is in `.superpowers/sdd/2026-09-16-academic-homepage-migration/cover_map.md`. Apply it verbatim: insert a `cover:` line into each listed file's front matter, aligned with the existing keys. All 25 target images already exist under `assets/images/covers/`.

The 7 files listed in `.superpowers/sdd/2026-09-16-academic-homepage-migration/no_cover.md` get NO cover key — the two theses (the owner asked for no thesis covers) and five entries that have neither a slide deck nor a hosted PDF.

- [ ] **Step 7: Rebuild and run the assertions**

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && rm -rf _site_t10 && bundle exec jekyll build -d _site_t10 2>&1 | tail -3
echo "--- broken logo imgs (expect 0) ---"; grep -c 'img src="" ' _site_t10/index.html
echo "--- bubble-hash placeholders (expect 0) ---"; grep -c "bubble-visual-hash" _site_t10/publications/index.html
echo "--- entries with covers (expect 30) ---"; grep -rc "^cover:" _publications | grep -v ":0" | wc -l
echo "--- every referenced cover resolves ---"
for p in $(grep -rhoE '/assets/images/covers/[A-Za-z0-9._-]+' _publications | sort -u); do test -f "_site_t10$p" && echo "OK $p" || echo "MISSING $p"; done | grep -c OK
for p in $(grep -rhoE '/assets/images/covers/[A-Za-z0-9._-]+' _publications | sort -u); do test -f "_site_t10$p" || echo "MISSING $p"; done
echo "--- single all-publications link on home ---"; grep -c "All publications" _site_t10/index.html
rm -rf _site_t10
```

Expected: `0` broken logo images, `0` bubble hashes, `30` entries with covers, every cover `OK` with no `MISSING`, and exactly `1` "All publications" link.

- [ ] **Step 8: Commit**

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && git commit _includes/widgets/experience_card.html _includes/widgets/publication_card.html _includes/widgets/publication_item.html _publications -m "$(cat <<'EOF'
Fix home-page cards and give publications consistent covers

Only render an institution logo when one is set, keep a single All
publications link, and show no placeholder graphic for entries that have
no cover.

Co-Authored-By: Claude Opus 5 (1M context) <noreply@anthropic.com>
EOF
)"
```

- [ ] **Step 3b: Replace the About Me bio**

The owner supplied new bio copy and asked for it to be merged with the existing text, written in the first person, and weighted toward her current interests: LLM AI agents, agentic GeoAI, Digital Earth, DGGS, and environmental modelling.

In `_data/profile.yml`, replace the entire `short_bio` value with:

```yaml
short_bio: >-
  <p>
    I am a Postdoctoral Associate at the University of Calgary, where I completed my Ph.D. in Geomatics
    Engineering. In December 2026, I join the <a href="https://www.uoguelph.ca/" target="_blank">University
    of Guelph</a> as an Assistant Professor in the Department of Geography, Environment &amp; Geomatics.
  </p>
  <p>
    My research develops agentic GeoAI, in which large language model (LLM) agents plan, reason, and act
    over geospatial data grounded in Discrete Global Grid Systems (DGGS). A DGGS gives spatial operations
    a consistent frame across resolutions, which supports an operational Digital Earth. I build geospatial
    intelligence frameworks that integrate multi-source spatial data with machine learning and AI agents,
    and I apply them to environmental and climate modelling, including methane emissions monitoring, flood
    risk assessment, and environmental resilience. My research interests also include geospatial data
    science, spatial data infrastructure, and geospatial decision-support systems.
  </p>
```

Keep the surrounding keys (`short_bio_text_justify`, `portrait_url`) untouched. Do not alter `positions:`, `education:`, or `experience:` — the incoming-appointment framing there is already correct and was reviewed.

Verify after building that the bio renders as two paragraphs and still contains no present-tense claim of the Guelph professorship:

```bash
cd /e/UCalgary_postdoc/Erin-1919.github.io && grep -c "agentic GeoAI" _site_t10/index.html && grep -ciE "is an assistant professor" _site_t10/index.html
```

Expected: `1` then `0`.
