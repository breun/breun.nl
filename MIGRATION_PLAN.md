# Jekyll to Hugo Migration Plan

This document outlines the step-by-step plan to migrate **breun.nl** from Jekyll to [Hugo](https://gohugo.io/).

---

## 1. Objectives & Guiding Principles

1. **Preserve Content & URLs**:
   - Keep post content in `_posts/` (or migrated to `content/posts/`) unchanged except for minimal front matter and template tag adjustments.
   - Maintain exact URL parity for all 537 existing posts (`/:year/:month/:title.html`), root pages, assets, and feeds.
2. **Embrace Hugo Standards**:
   - Use Hugo's standard `public/` directory for output (`publishDir`), adjusting `./deploy` to sync from `public/`.
3. **Clean Architecture**:
   - Modern Hugo templating using `baseof.html`, single/list templates, custom shortcodes for embeds, and native RSS feeds.
   - Elimination of Ruby/Bundler dependencies.

---

## 2. Current State vs. Target Hugo State

| Aspect | Current Jekyll Setup | Target Hugo Setup | Notes |
| :--- | :--- | :--- | :--- |
| **Engine** | Jekyll 4.x (Ruby) | Hugo v0.167+ (Go) | Instant builds (<100ms) without Ruby runtime |
| **Config** | `_config.yml` | `hugo.yaml` | Base URL, Dutch locale, permalinks, mounts, uglyURLs |
| **Content Directory** | `_posts/` (537 files: 483 `.markdown`, 54 `.html`) | `_posts/` mounted as `content/posts` (or `content/posts/`) | Zero file renaming required |
| **Permalinks** | `/:year/:month/:title.html` | `/:year/:month/:slug` with `uglyURLs: true` | Generates identical `YYYY/MM/post-slug.html` files |
| **Layouts** | `_layouts/default.html`, `post.html` | `layouts/_default/baseof.html`, `single.html`, `index.html` | Hugo Go template syntax |
| **Includes** | `_includes/youtube.html` | `layouts/shortcodes/youtube.html` | Replaces `{% include youtube.html %}` (6 occurrences) |
| **Assets** | `css/`, `favicons/`, `images/`, `files/`, `.well-known/`, `.htaccess` | Hugo `static/` or module mounts | Copied verbatim to `public/` |
| **Output Directory** | `_site/` | `public/` (Hugo default) | `./deploy` script updated to `SOURCE=public/` |
| **RSS Feed** | `feed.xml` | `layouts/_default/rss.xml` (output format baseName: `feed`) | Output at `/feed.xml` |

---

## 3. Detailed Content & Front Matter Analysis

An audit of the 537 posts in `_posts/` revealed:

1. **Front Matter Fields Present**:
   - `layout: post` (537 files): In Hugo, layouts are inferred from the section (`posts`), so this field can remain in place or be ignored.
   - `title:` (537 files): Standard in Hugo.
   - `date:` (519 files): Formatted as `'YYYY-MM-DD HH:MM:SS +0100'`.
   - `mt_id:` (519 files): Legacy Movable Type IDs, safely parsed as custom Hugo page params (`.Params.mt_id`).
   - `categories:` (518 files): Parsed as taxonomy terms.
2. **Posts without explicit `date` field (18 files)**:
   - In Jekyll, dates for files like `2014-01-01-orkest-nota-bene-speelt-helden.markdown` were inferred from the filename.
   - In Hugo, configuring `frontmatter.date: [":filename", "date", "publishDate"]` handles this automatically without requiring manual edits to post front matter.
3. **Liquid Tags in Content**:
   - Only **6 instances** of `{% include youtube.html id="..." title="..." %}` exist across 3 files:
     - `_posts/2006-11-01-brian-wilco.markdown` (1)
     - `_posts/2007-04-03-irack.markdown` (1)
     - `_posts/2007-05-31-happy-together.markdown` (1)
     - `_posts/2026-02-07-thistle-sifter-forever-the-optimist.markdown` (3)
   - These will be migrated to Hugo shortcode syntax: `{{< youtube id="..." title="..." >}}`.

---

## 4. Target Directory Structure

```text
.
├── hugo.yaml                     # Replaces _config.yml
├── build                         # Updated to run 'hugo'
├── deploy                        # Updated: SOURCE=public/
├── content/                      # Content root (or _posts mounted via hugo.yaml)
│   └── posts/                    # 537 Markdown & HTML post files
├── layouts/
│   ├── _default/
│   │   ├── baseof.html           # Base layout (header, footer, webfonts)
│   │   ├── single.html           # Post layout (Dutch date formatting, prev/next)
│   │   ├── list.html             # Fallback list layout
│   │   └── rss.xml               # Custom RSS template for feed.xml
│   ├── index.html                # Homepage layout (post listing)
│   └── shortcodes/
│       └── youtube.html          # Responsive YouTube embed shortcode
├── static/                       # Static assets copied directly to public/
│   ├── .htaccess
│   ├── .well-known/
│   ├── css/
│   │   ├── main.css
│   │   └── syntax.css
│   ├── favicons/
│   ├── files/
│   └── images/
```

> **Note on Content Strategy**: 
> You can choose between:
> - **Option A (Standard Hugo)**: Move `_posts` to `content/posts/` and static folders to `static/`.
> - **Option B (Hugo Mounts)**: Keep `_posts/`, `css/`, `images/`, etc., in place and map them via Hugo `module.mounts` in `hugo.yaml`.
> 
> *Recommendation*: **Option A** is the standard Hugo convention and avoids complex mount configurations.

---

## 5. Hugo Configuration Specification (`hugo.yaml`)

```yaml
baseURL: "https://breun.nl/"
title: "breun"
languageCode: "nl-NL"
defaultContentLanguage: "nl"
uglyURLs: true

# Extract date from filename if missing from front matter
frontmatter:
  date:
    - ":filename"
    - "date"
    - "publishDate"

# Match Jekyll URL scheme /:year/:month/:title.html
permalinks:
  posts: /:year/:month/:slug

# Disable taxonomy pages if not used on the live site
disableKinds:
  - taxonomy
  - term

# Custom RSS output file matching feed.xml
outputFormats:
  RSS:
    baseName: "feed"

outputs:
  home:
    - HTML
    - RSS
  page:
    - HTML
  section: []

params:
  subtitle: 'Ask yourself: "What am I doing here?"'
  author: "Nils Breunese"
```

---

## 6. Template Conversion Specifications

### 6.1 Base Layout (`layouts/_default/baseof.html`)
Replaces `_layouts/default.html`:
- Retains identical `<head>` tags, web fonts, CSS links (`/css/syntax.css`, `/css/main.css`), and RSS link (`/feed.xml`).
- Retains social media header contact blocks and footer copyright.
- Embeds page content via `{{ block "main" . }}{{ .Content }}{{ end }}`.

### 6.2 Single Post Layout (`layouts/_default/single.html`)
Replaces `_layouts/post.html`:
- **Title & Dutch Date Formatting**: Uses Hugo's localized time format:
  ```html
  <main>
    <article>
      <header>
        <h1>{{ .Title }}</h1>
        <time datetime="{{ .Date.Format "2006-01-02" }}">
          {{ .Date.Format "2 January 2006" }}
        </time>
      </header>
      {{ .Content }}
    </article>
    <nav class="post">
      {{ with .PrevInSection }}
      &laquo; <a rel="prev" href="{{ .RelPermalink }}">{{ .Title }}</a>
      {{ end }}
      {{ if and .PrevInSection .NextInSection }}
      &mdash;
      {{ end }}
      {{ with .NextInSection }}
      <a rel="next" href="{{ .RelPermalink }}">{{ .Title }}</a> &raquo;
      {{ end }}
    </nav>
  </main>
  ```
  *(Note: Hugo `.Date.Format "2 January 2006"` automatically formats month names in Dutch when `defaultContentLanguage = "nl"`).*

### 6.3 Homepage (`layouts/index.html`)
Replaces `index.html`:
```html
{{ define "main" }}
<nav class="posts">
  <ul>
    {{ range where site.RegularPages "Section" "posts" }}
    <li>
      <span>{{ .Date.Format "2006-01-02" }}</span> &raquo; 
      <a href="{{ .RelPermalink }}">{{ .Title }}</a>
    </li>
    {{ end }}
  </ul>
</nav>
{{ end }}
```

### 6.4 YouTube Shortcode (`layouts/shortcodes/youtube.html`)
Replaces `_includes/youtube.html`:
```html
<div class="youtube-container">
    <iframe src="https://www.youtube.com/embed/{{ .Get "id" }}"
            title="{{ .Get "title" | default "YouTube video" }}"
            frameborder="0"
            allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
            allowfullscreen>
    </iframe>
</div>
```

### 6.5 RSS Feed (`layouts/_default/rss.xml`)
Replaces `feed.xml`:
Generates valid RSS 2.0 XML with Atom link `/feed.xml` and the 10 most recent posts, matching the exact format of the current Jekyll feed.

---

## 7. Step-by-Step Migration Roadmap

### Phase 1: Preparation & Configuration
1. Create `hugo.yaml` with the permalinks, localization, output formats, and uglyURLs configuration.
2. Update `.gitignore`:
   - Replace `_site/` with `public/`.
   - Add `.hugo_build.lock` and `resources/_gen/`.

### Phase 2: Static Assets & Content Structure
1. Reorganize directory structure (or setup mounts):
   - Move static asset directories (`css/`, `favicons/`, `images/`, `files/`, `.well-known/`, `.htaccess`) to `static/`.
   - Rename/move `_posts/` to `content/posts/`.
2. Convert the 6 YouTube include tags in `_posts/` to `{{< youtube ... >}}`.

### Phase 3: Templates Implementation
1. Create `layouts/_default/baseof.html` based on `_layouts/default.html`.
2. Create `layouts/_default/single.html` based on `_layouts/post.html`.
3. Create `layouts/index.html` based on `index.html`.
4. Create `layouts/shortcodes/youtube.html`.
5. Create `layouts/_default/rss.xml`.

### Phase 4: Build & Deploy Script Updates
1. Update `./build` script to execute `hugo`.
2. Update `./deploy` script: change `SOURCE=_site/` to `SOURCE=public/`.
3. Run `hugo` to generate `public/`.
4. Perform parity testing:
   - Verify count of generated HTML files (537 post pages + index).
   - Compare HTML output and URL structure against Jekyll's generated `_site/`.
   - Verify `/feed.xml` validity and content.
   - Verify localized date strings (e.g. `7 februari 2026`).

### Phase 5: Cleanup
1. Remove Jekyll-specific files:
   - `_layouts/`, `_includes/`, `_config.yml`, `_config.yml.private`, `Gemfile`, `Gemfile.lock`, `.ruby-version`, `.jekyll-cache/`, and old `_site/`.
2. Verify that `./deploy` syncs `public/` to production seamlessly.

---

## 8. Verification & Diffing Strategy

Before running `deploy`, run an automated comparison between the Jekyll build and Hugo build:
1. Ensure the existing Jekyll output exists in `_site/`.
2. Run `hugo` to generate `public/`.
3. Run a comparison script to verify:
   - Every file path present in `_site/` exists in `public/`.
   - Feed XML at `public/feed.xml` matches structure and content.
   - Assets and images in `public/` match 1-to-1.
