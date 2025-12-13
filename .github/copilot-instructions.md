# Copilot Instructions for 10Corp Hugo Site

## Project Overview
This is a **Hugo static site generator** project for 10Corp, a web design company. The site contains business pages, portfolio, blog, and extensive legal/terms content. Hugo compiles markdown content + theme layouts into static HTML served from the `public/` directory.

**Key Command**: `hugo.exe server` (dev), `hugo.exe` (production build)

## Architecture

### Content Structure (`content/`)
- **Root pages**: `about/`, `services/`, `pricing/`, `contact/`, `portfolio/`, `blog/`, `websites/`, `hosting/`, `domains/`, `email/`, `security/`, `marketing/`
- **Legal content**: `legal/` contains ~25 subsections (terms-of-service, privacy-policy, refund-policy, domain-name-registration-agreement, hosting-agreement, etc.)
- **Content format**: Markdown files with YAML frontmatter; directory structure maps to URL paths
- **Naming convention**: `index.md` in directories creates section pages; nested folders create subsections

### Theme System
- **Active theme**: `terio` (located in `themes/terio/`)
- **Theme structure**: Layouts in `themes/terio/layouts/`, assets/CSS in `themes/terio/assets/`, example site in `themes/terio/exampleSite/`
- **Custom layouts**: Site-specific overrides in root `layouts/` override theme layouts
- **Project layouts**: Check `layouts/` before modifying theme files

### Configuration
- **`config.toml`**: Main Hugo config with site title, baseURL, theme selection, menu structure, pagination settings
- **Menu hierarchy**: Defined in `config.toml` with parent-child relationships (e.g., Pages > About, Pages > Services)

## Content Patterns

### Frontmatter Convention
All pages use this structure:
```yaml
---
title: "Page Title"
seoTitle: "SEO-optimized title for search engines"
description: "Meta description for SEO"
keywords:
  - "keyword1"
  - "keyword2"
image: "/images/image-path.png"
builder: true  # Indicates content is managed/visible
date: YYYY-MM-DDTHH:MM:SS+00:00
---
```
Example: `content/legal/additional-renewal-terms/index.md`

### Legal Pages Pattern
Legal content uses numbered sections with subsections. Last line includes: `**Last Modified**: MMM DD, YYYY`
Example: `content/legal/terms-of-service/index.md`

### Homepage Sections
Homepage (`_index.md`) uses `sections:` array to define page layout blocks:
- hero-slider, marketing-one/two, brands-two, services, numbers, projects-featured, testimonial-two, team-one, blog-carousel-two, cta-two

## Data & Internationalization
- **Data files**: `data/` directory (check for site metadata, lists, configurations)
- **i18n files**: `i18n/` contains language/translation strings
- **Default language**: English (`en`), configured in `config.toml`

## Static Assets
- **`static/`**: Direct copy to public root (images, files, scripts)
- **`assets/`**: Compiled/processed assets (SCSS, JS) via Hugo pipes
- **Image paths**: Reference as `/images/` in markdown; images stored in `static/images/`

## Build & Development Workflow

### Local Development
```bash
cd d:\Hugo\bin
hugo.exe server
```
Watches for changes, live-reloads at `http://localhost:1313`

### Production Build
```bash
cd d:\Hugo\bin
hugo.exe
```
Generates optimized static site in `public/` directory

### Netlify Deployment
- `netlify.toml` present; site deploys to production via Netlify on push

## Critical Patterns & Conventions

1. **Markdown frontmatter is mandatory** for all content to be properly rendered and indexed
2. **Directory structure = URL structure**: `content/about/team/index.md` → `/about/team/`
3. **SEO metadata**: Always populate `seoTitle`, `description`, `keywords`, and `image` fields
4. **Date format**: ISO 8601 with timezone (`YYYY-MM-DDTHH:MM:SS+00:00`)
5. **Theme overrides**: Place custom HTML/CSS in root `layouts/` or `assets/`, not in theme directory
6. **Hugo variable references**: Use `{{ .Site.BaseURL }}`, `{{ .Title }}`, `{{ .Date }}` in templates

## Integration Points
- **Netlify deployment**: Configured in `netlify.toml` (builds with Hugo)
- **Theme inheritance**: Terio theme provides base templates; check `themes/terio/layouts/` before creating overrides
- **No external APIs or databases**: Static generation only; content is version-controlled markdown

## Common Tasks
- **Add new page**: Create directory in `content/` with `index.md` containing frontmatter + markdown
- **Update legal content**: Edit existing markdown in `content/legal/*/index.md`; preserve frontmatter format
- **Modify navigation**: Update menu structure in `config.toml`
- **Change home layout**: Modify `sections:` array in `content/_index.md`
- **Deploy changes**: Push to repository; Netlify auto-builds via Hugo

---
Last updated: December 3, 2025
