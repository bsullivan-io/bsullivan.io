# bsullivan.io — Project Reference

## Overview

Personal portfolio and resume website for Brian Sullivan, a full-stack web engineer with 15+ years of experience. Hosted at **bsullivan.io** via GitHub Pages. The home page is a **services site** for small businesses (retro typographic style, sans-serif type), while the resume page keeps a dark terminal/hacker aesthetic, with a separate print-optimized layout.

---

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Static site generator | Jekyll (GitHub Pages compatible) |
| Templating | Liquid |
| Styling | SCSS (compiled by Jekyll, compressed output) |
| Markdown | Kramdown |
| JavaScript | Vanilla JS, inline in `home.html` only (scroll reveal); no build step, no dependencies |
| Hosting | GitHub Pages (auto-deploy on push to `main`) |
| Domain | bsullivan.io (via `CNAME` file) |

---

## Local Development

**Prerequisites:** Ruby, Bundler

```bash
# Install dependencies
bundle install

# Start local dev server (http://localhost:4000)
bundle exec jekyll serve

# Build static output to _site/
bundle exec jekyll build
```

> **Note:** Changes to `_config.yml` require restarting the Jekyll server to take effect. Changes to other files hot-reload automatically.

---

## Project Structure

```
bsullivan.io/
├── _config.yml              # Site config, resume personal info, section toggles, social links
├── _data/                   # YAML content files (resume data — edit these to update resume)
│   ├── experience.yml       # Work history
│   ├── skills.yml           # Technical skills by category
│   ├── education.yml        # Degrees and awards
│   ├── projects.yml         # Personal projects
│   ├── interests.yml        # Outside interests
│   ├── associations.yml     # Volunteer/org memberships (currently hidden)
│   ├── recognitions.yml     # Awards (currently hidden)
│   └── links.yml            # Additional links (currently hidden)
├── _includes/               # Reusable Liquid partials
│   ├── head.html            # <head> section
│   ├── icon-links.html      # Social media icon row
│   ├── print-social-links.html
│   └── icons/               # Individual SVG icon partials (GitHub, LinkedIn, etc.)
├── _layouts/                # Page layout templates
│   ├── home.html            # Services home page (inline CSS + JS)
│   ├── resume2.html         # Dark terminal resume (ACTIVE layout for /resume)
│   ├── resume_print.html    # Print/PDF-optimized resume
│   └── resume.html          # White professional resume (alternate, not currently active)
├── _sass/                   # SCSS partials
│   ├── _variables.scss      # Colors, typography, spacing
│   ├── _mixins.scss         # Reusable mixins (media queries, typography helpers)
│   ├── _normalize.scss      # CSS reset
│   ├── _base.scss           # Base element styles
│   ├── _layout.scss         # Grid and column system
│   └── _resume.scss         # Resume-specific component styles
├── css/
│   └── main.scss            # SCSS entry point (imports all partials)
├── _assets/                 # Design source files (Sketch, AI — not served)
├── images/                  # Served images (avatar, backgrounds, PDF export)
├── resume/
│   └── index.html           # Resume page (front matter only — uses resume2 layout)
├── index.html               # Home page (uses home layout)
├── 404.html                 # 404 error page
├── Gemfile                  # Ruby dependencies
└── CNAME                    # Custom domain declaration
```

---

## Layouts

### `home.html` — Services Home Page
- Single-page marketing site for Brian's web & technology services for small businesses
- Retro / typographic / gridded style (inspired by GASS Records, Mecha, App State, Rapide on Awwwards/Httpster): thick graphite rules, pill buttons and labels, big condensed type, checkerboard strips, concentric-ring op-art
- Palette tokens on `:root`: `--teal #177e89`, `--dteal #084c61`, `--scarlet #db3a34`, `--gold #ffc857`, `--graphite #323031`, on a warm `--paper #f6f0e4` with a subtle grain/fibre card-stock texture
- Fonts (Google Fonts): **Archivo** variable (uses the `wdth` axis for condensed display type) + **IBM Plex Mono** for small labels
- Sections: top bar, split hero (copy + teal art panel with code photo, spinning badge and a tilting business card using `images/avatar.jpg`), two marquee bands, photo/color mosaic, services (banner + 6 rows), care plans, process, portfolio showcase (JS slider, stacked without JS), about collage, contact, checker strip + footer
- **Portfolio** loops over `_data/projects.yml`, filtered by the `showcase` Liquid assign (`"Make a Mile,newsquick.app"`)
- Stock photos are free-license Unsplash images saved in `images/stock/` (screens show code, dashboards or websites, never a blank desktop); `.duo`, `.duo-red`, `.duo-teal`, `.duo-gray` tint them into the palette and hover restores color
- Self-contained: inline CSS and small inline JS (scroll reveal, card tilt, project slider); respects `prefers-reduced-motion`
- Copy style: plain and factual; avoid em dashes, "not X, Y" constructions, and location references (no town names)
- `/services/` redirects to `/#services`

### `resume2.html` — Terminal Resume (active)
- The layout used by `resume/index.html`
- Dark terminal aesthetic applied to full resume content
- Renders all enabled sections from `_data/` and `_config.yml`

### `resume_print.html` — Print / PDF Resume
- Clean two-column layout, white background
- `@media print` CSS included
- Used for PDF export (output saved at `images/Resume (Print).pdf`)
- No decorative elements or background patterns

### `resume.html` — Professional Resume (alternate)
- White background with triangle pattern
- Schema.org microdata for SEO
- Contact button (shown when `resume_looking_for_work: "yes"` in config)
- Alternate theme; not the active layout but maintained for reference

---

## Updating Resume Content

### Personal info & section visibility → `_config.yml`

```yaml
resume_name:            "Brian Sullivan"
resume_title:           "Full Stack Developer"
resume_contact_email:   "brian@bsullivan.io"
resume_header_intro:    "<p>Your intro here.</p>"
resume_looking_for_work: "yes"   # "yes" | "no" | remove key for blank

# Toggle sections (true = visible, false = hidden)
resume_section_experience:   true
resume_section_education:    true
resume_section_projects:     true
resume_section_skills:       true
resume_section_recognition:  false
resume_section_links:        false
resume_section_associations: false
resume_section_interests:    true
```

### Work history → `_data/experience.yml`

```yaml
- company: "Company Name"
  position: "Your Title"
  duration: "Month Year - Month Year"
  summary: "<ul><li>Bullet point</li></ul>"
```

### Skills → `_data/skills.yml`

```yaml
- skill_category: "Category Name"
  skills:
    - name: "Skill Name"
```

### Education → `_data/education.yml`

```yaml
- degree: "Degree Name"
  university: "University Name"
  year: "Graduation Year"
  description: "Optional note"
```

### Projects → `_data/projects.yml`

```yaml
- project: "Project Name"
  role: "Founder, Developer"
  duration: "2025 &mdash; Present"
  url: "https://projecturl.com"
  image: "/images/projects/projectname.png"   # optional thumbnail (home page)
  description: "Description"
```

> This file feeds **both** the resume projects section and the home-page
> "Selected work" section. To feature a project as a window on the home page, add its
> exact `project:` name to the `showcase` list in `_layouts/home.html`.
> Thumbnails are screenshots saved under `images/projects/`.

---

## Styling & Themes

The site has these distinct visual themes:

| Theme | Used in | Description |
|-------|---------|-------------|
| Retro typographic services | `home.html` | Teal / scarlet / gold / graphite on textured paper, Archivo + IBM Plex Mono, pills, marquees, checker strips |
| Terminal | `resume2.html` | Dark bg, green monospace text, fake terminal window chrome |
| Professional | `resume.html` | White bg, serif/sans-serif, triangle pattern, contact button |
| Print | `resume_print.html` | Two-column, minimal, black & white, `@media print` optimized |

**SCSS structure:** `css/main.scss` imports `_variables → _normalize → _base → _layout → _resume`.

**Mobile breakpoint:** 600px for the resume/SCSS pages (defined in `_sass/_mixins.scss` as `media_larger_than_mobile`). The home page is self-contained with breakpoints at 1080px, 960px, 760px and 480px.

---

## Deployment

Push to the `main` branch on GitHub — GitHub Pages automatically builds and deploys. No CI/CD configuration needed. Build output (`_site/`) is gitignored.

SSL is provided automatically by GitHub Pages for the custom domain.

---

## Active Resume Content (as of 2026-03-26)

**Experience:** 5 positions (2010–2025)
- Marketfuel — Senior Full-Stack Web Engineer (Apr 2024–Oct 2025)
- Flashtalking by Mediaocean — Director, Feeds Automation & Engineering (Feb–Sep 2023)
- Mediaocean — Senior Web Services Engineer (May 2015–Feb 2023)
- Theatermania — Full-Stack Web Developer (May 2013–Nov 2014)
- Inkwell Global Marketing — Full-Stack Web Developer (Jun 2010–Mar 2013)

**Visible sections:** Experience, Skills, Education, Projects, Interests
**Hidden sections:** Recognition, Links, Associations
