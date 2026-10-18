# Nolan Townsend — Water Resources • GIS • Data

Personal site of Nolan Townsend, senior water resources analyst at the City of Westminster, Colorado. Built with [Hugo](https://gohugo.io/) and deployed to GitHub Pages.

The design draws on John Wesley Powell's 1890 *Arid Region of the United States, Showing Drainage Districts*: parchment tones, district colors, topographic contours and a homepage "river log" where the newest work sits upstream.

**Live site:** https://&lt;your-username&gt;.github.io/

First-time setup and GitHub Pages configuration are covered in [SETUP.md](SETUP.md).

---

## Quick start

```bash
# run locally (Hugo extended, any recent version)
hugo server
# open http://localhost:1313

# production build (output in ./public)
hugo --gc --minify
```

Pushing to `main` publishes automatically through `.github/workflows/hugo.yml`.

---

## Repository layout

```
.
├── .github/workflows/hugo.yml   # build + deploy to GitHub Pages
├── assets/css/powell.css        # all site styles (palette, type, layouts)
├── content/
│   ├── about.md
│   ├── field-notes/             # project write-ups
│   └── resources/               # articles, guides, how-tos
├── layouts/
│   ├── _default/baseof.html     # page shell; picks the layout
│   ├── _default/list.html       # section + category listing pages
│   ├── _default/single.html     # individual pages
│   ├── index.html               # homepage
│   ├── 404.html
│   └── partials/powell/         # header, footer, river log, cards, compass, etc.
├── static/
│   ├── img/                     # Powell map, topo artwork, your images
│   └── js/riverlog.js           # preview-pane hover (optional enhancement)
├── hugo.toml                    # site configuration
├── preview.html                 # static design preview (ignored by Hugo)
├── README.md
└── SETUP.md
```

---

## Writing content

### Field Notes (projects)

Create a file in `content/field-notes/`:

```bash
hugo new field-notes/my-project.md
```

```toml
+++
title = 'Standley Lake Storage Analysis'
date = '2026-10-01'
categories = ['Hydrology']                 # first category sets the color
tools = ['Hydrology', 'Power BI', 'Python']
summary = 'One or two sentences shown on the homepage.'
image = '/img/field-notes/standley-lake.jpg'
featured = true                            # used by the Atlas layout
+++

Write-up in Markdown.
```

### Resources (articles)

```bash
hugo new resources/my-article.md
```

```toml
+++
title = 'Drought Conditions in Colorado'
date = '2026-10-01'
categories = ['Drought']
summary = 'Optional. Falls back to the opening of the article.'
+++
```

### CV

`content/resume.md` is rendered by `layouts/_default/resume.html` (set by `layout = 'resume'` in its front matter) at `/resume/`. Edit it like any Markdown page. The page has a print stylesheet, so **Print → Save as PDF** gives a clean copy. To offer a downloadable PDF instead, put the file in `static/` and add `pdf = '/Nolan-Townsend-CV.pdf'` to the front matter.

### Images

Put images in `static/img/` and reference them from the site root, e.g. `/img/field-notes/standley-lake.jpg`. Items without an `image` show a neutral placeholder.

### Drafts

Add `draft = true` to keep a page out of the published site. Preview drafts locally with `hugo server -D`.

---

## Homepage river log

The **Recent Work** section mixes the newest Field Notes and Resources:

- Newest items sit **upstream**. River miles count down toward the mouth (RM 0.0), following the hydrologic convention that river miles increase upstream.
- Each node takes the color of the item's first category.
- The legend lists every category with a post count and links to its category page.

Settings in `hugo.toml`:

| Key | Default | What it does |
| --- | --- | --- |
| `riverlogCount` | `4` | Number of items shown |
| `riverMileStep` | `2.5` | River-mile spacing between items |
| `riverlogStyle` | `"rows"` | `rows`: title, summary and image across the page. `preview`: sticky detail pane that follows hover or focus |

---

## Categories and colors

Colors come from the Powell map's district tints. Keys are lowercase category names:

```toml
[params.powell.categoryColors]
hydrology = "#7aaec6"
drought = "#c99a3a"
groundwater = "#b8643c"
gis = "#7a8a3e"
"data & tools" = "#737a90"
climate = "#c4807a"
research = "#5a8a8a"
```

New categories show up in the legend automatically. Categories without a color entry fall back to sand (`#c9b98a`).

---

## Configuration reference

Everything lives under `[params.powell]` in `hugo.toml`.

| Key | Purpose |
| --- | --- |
| `layout` | Homepage layout: `expedition` (current), `atlas` or `fieldnotes` |
| `name`, `tagline` | Wordmark and subtitle in the header |
| `coordinates` | Shown in the header (Field Notes layout) and panorama strips |
| `heroImage`, `heroAlt` | Hero map image and its alt text |
| `mapTitle`, `mapAuthor`, `mapCredit` | Map caption and attribution |
| `[params.powell.hero]` | Eyebrow, title, intro text and button for the homepage |
| `[params.powell.heroByLayout.<layout>]` | Per-layout overrides for the hero text |
| `[params.powell.about]` | About block (Atlas layout) |
| `[params.powell.panorama]` | Optional engraving strip; empty shows topo lines |
| `[params.powell.quote]` | Quote band text and attribution |
| `[[params.powell.social]]` | Footer links |

Navigation is set in `[menus]`: Home, About, Field Notes, Resources, Contact.

---

## Design system

**Type:** Cormorant Garamond (display), Crimson Text (body), Space Mono (labels and data), loaded from Google Fonts.

**Palette** (CSS custom properties in `assets/css/powell.css`):

| Token | Hex | Use |
| --- | --- | --- |
| `--paper` | `#efe4cc` | Page background |
| `--ink` | `#2b2418` | Primary text |
| `--terra` | `#9f4f2c` | Links, buttons, active states |
| `--rule` | `#c6b38c` | Dividers |
| `--dark` | `#2d2920` | Dark bands (Atlas, Field Notes sidebar) |
| channel blue | `#3f78a6` | River line and river miles |

**Accessibility:** text meets WCAG AA contrast on parchment, interactive targets are at least 44px, focus is always visible, there's a skip-to-content link, and category colors are always paired with a text label.

**Responsive:** the river log stacks its intro above the list below 1180px and collapses to one column below 900px.

---

## Credits and licensing

- **Hero map:** J.W. Powell, *Arid Region of the United States, Showing Drainage Districts*, USGS Eleventh Annual Report, 1890. High-resolution scan by Torpyl via Wikimedia Commons, licensed **CC BY-SA 4.0**. Keep the credit in `mapCredit`.
- **Topographic artwork** (`static/img/topo-*.svg`): generated for this site.
- **Fonts:** Cormorant Garamond, Crimson Text and Space Mono are licensed under the SIL Open Font License.
- **Quote:** John Wesley Powell, 1893 International Irrigation Congress, Los Angeles.

Site code and content © Nolan Townsend.
