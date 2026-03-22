# Project Description

## How this project is built and run

### Architecture

This is a **Cloudflare Worker** project that serves a static portfolio site at `alexlerikos.me`. The Worker (`src/index.js`) handles HTTP requests, maps the hostname to a content directory under `public/`, and serves static assets via Cloudflare's asset binding.

### Content structure

```
public/alexlerikos.me/          ← content root for alexlerikos.me
├── index.md                    ← article list only (auto-managed by site-tool)
├── index.template.html         ← full homepage shell (sidebar, sections, $body$ slot)
├── index.html                  ← GENERATED — do not hand-edit
├── style.css                   ← all styling (palette, sidebar, layout, responsive)
├── writing/
│   ├── article.template.html   ← shared template for all articles
│   └── */index.md → index.html ← each article
├── projects/
│   ├── index.template.html
│   └── index.md → index.html
└── feed.xml                    ← RSS feed (generated alongside index.md)
```

### Build command

From the site content root:

```sh
make -C public/alexlerikos.me public
```

This runs `site-tool gen-toc` (updates the article list in `index.md` and generates `feed.xml`), then runs pandoc on every `.md` file to produce `.html` files.

### Dev server

```sh
make -C maint serve
```

This starts `wrangler dev` on `0.0.0.0`. Since the Worker routes by hostname, use `?d=alexlerikos.me` to tell it which site to serve when accessing via `localhost:8787`.

### What is `index.template.html`?

It's a **pandoc template** — the full HTML shell of the homepage. It contains:

- **`<head>`** — charset, viewport, favicon links, `style.css`, RSS alternate link
- **Sidebar** (`<aside class="sidebar">`) — profile photo, name, title, social links, nav links (Overview, Experience, Projects, Writing, Skills, Contact), RSS button
- **Main content** (`<main class="index-main">`) with static HTML sections:
  - Breadcrumb
  - Overview (hero headline, bio, tags, links + focus areas sidebar)
  - Experience timeline (job history entries)
  - Project cards (2-column grid)
  - **`$body$` slot** — this is where pandoc injects the rendered content from `index.md`
  - Skills section (progress bars + tech stack grid)
  - Footer (copyright + links)

The `$body$` variable is pandoc's template mechanism. When pandoc processes `index.md` (which contains only the article list), it renders that markdown to HTML and substitutes it into the `$body$` slot in the template. The result is `index.html`.

So the division is:
- **`index.template.html`** = everything static on the homepage (sidebar, experience, projects, skills, footer)
- **`index.md`** = only the dynamic article list (auto-updated by `site-tool gen-toc` whenever articles are added/removed)
- **`index.html`** = the generated output — never hand-edit this file

The static sections currently contain `AI GEN PLACEHOLDER:` prefixed content, indicating they need to be replaced with real content by the author. Those edits happen in `index.template.html`, then `make -B index.html` regenerates the output.
