# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a **Quarto-based academic personal website** for a university professor. The site includes bio, publications, teaching, research, students, service activities, and talks.

The site is hosted on GitHub Pages and deploys from the `docs/` directory (not the typical `_site/` output).

## Build Commands

### Preview the site locally
```bash
quarto preview
```

### Build the site for production
```bash
quarto render
```
This generates the static site in the `docs/` directory (configured in `_quarto.yml` via `output-dir: docs`).

### Check Quarto version
```bash
quarto --version
```

## Architecture

### Site Structure

- **`_quarto.yml`**: Main configuration file defining:
  - Project type and output directory (`docs/`)
  - Navigation bar structure and links
  - HTML format settings (CSS, TOC, header includes)
  - Website metadata (title, footer)

- **`*.qmd` files**: Quarto Markdown source files for each page
  - `index.qmd`: Homepage with about section and recent publications listing
  - `bio.qmd`, `contact.qmd`, `teaching.qmd`, `research.qmd`, `service.qmd`, `students.qmd`: Content pages
  - `publications/index.qmd`: Publications page with multiple filtered listings
  - `talks/index.qmd`: Talks/presentations page
  - `teoria-colas.qmd`: Queueing theory course materials (Spanish)
  - `news-archive.qmd`: Archive of older news items

- **`publications/papers.yml`**: Single YAML file containing all publications with metadata:
  - Structured with fields: `title`, `authors`, `publication`, `year`, `type`, `categories`, `path`
  - Types include: `journal`, `selected_conf`, `other_conf`, `book_chapter`
  - Categories used for filtering (e.g., JCR, Machine Learning, 5G/6G)

- **`docs/`**: Output directory for the rendered static site (committed to git for GitHub Pages)

- **`_site/`**: Alternative output location (gitignored, not used for deployment)

### Publications System

The publications are managed through a **centralized YAML file** (`publications/papers.yml`) and rendered using Quarto's listing feature:

1. **Single source of truth**: All papers in `publications/papers.yml`
2. **Multiple filtered views**:
   - Homepage shows 5 most recent (`max-items: 5`)
   - Publications page shows separate sections for journals, selected conferences, other conferences, and book chapters
   - Filtering by `type` field in the YAML
3. **Custom styling**: Inline CSS in `publications/index.qmd` for table appearance

### Navigation

The navbar is defined in `_quarto.yml` with:
- UC3M navy blue background (`#002b54`)
- Dark theme for white text
- Left-aligned page links
- Right-aligned social/academic profile icons (Google Scholar, GitHub)

### Styling

- **`styles.css`**: Custom CSS for the site
- **`header.html`**: Additional HTML injected into the header (included via `_quarto.yml`)

## Common Workflows

### Adding a New Publication

1. Edit `publications/papers.yml`
2. Add entry with required fields: `title`, `authors`, `publication`, `year`, `type`, `categories`, `path`
3. Choose appropriate `type`: `journal`, `selected_conf`, `other_conf`, or `book_chapter`
4. Run `quarto render` to rebuild

### Adding a New Page

1. Create `pagename.qmd` in root directory
2. Add front matter with `title` and other metadata
3. Add to navbar in `_quarto.yml` under `website.navbar.left`
4. Run `quarto render`

### Updating News

- Edit `index.qmd` to update the "Latest News" section
- Move old news items to `news-archive.qmd` periodically

## Deployment

The site deploys to GitHub Pages from the `docs/` directory on the `main` branch. After making changes:

1. Run `quarto render` to build the site
2. Commit changes including the updated `docs/` directory
3. Push to GitHub - changes will be live automatically

## File Organization

- **PDFs**: Stored in `pdfs/` directory (certificates, awards, etc.)
- **Images**: Stored in `images/` directory
- **Profile photo**: `profile.jpg` in root
- Both `pdfs/` and `images/` are duplicated in `docs/` for the built site
