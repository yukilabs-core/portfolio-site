# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Purpose

Portfolio website for yukilabs-core, showcasing projects and accomplishments. Built with Astro for fast static site generation with optional interactive components.

## Development Commands

| Command | Purpose |
|---------|---------|
| `npm run dev` | Start local dev server at `http://localhost:4321` |
| `npm run build` | Build production-optimized site to `./dist/` |
| `npm run preview` | Preview production build locally before deploying |
| `npm run astro add <integration>` | Add Astro integrations (React, Vue, etc.) |
| `npm run astro check` | Run type checking |

## Project Structure

- **`src/pages/`** — Routes. Each `.astro` or `.md` file becomes a page (file-based routing)
- **`src/components/`** — Reusable Astro/React/Vue components
- **`src/layouts/`** — Layout components for page templates
- **`public/`** — Static assets (images, fonts, etc.) served as-is
- **`astro.config.mjs`** — Astro configuration

## Architecture Notes

- Astro renders pages to static HTML at build time, with optional island-based interactivity
- Pages are `.astro` files (Astro's template syntax) or Markdown
- Use `<Fragment>` or `<>` in Astro files to avoid extra wrapper elements
- Import styles inline with `<style>` tags or link external stylesheets

## Deployment

Built site (`./dist/`) is deployed to Cloudflare. Run `npm run build` locally to test before pushing.

## GitHub Setup

- Repository: `git@github.com:yukilabs-core/portfolio-site.git`
- SSH key: `~/.ssh/id_ed25519`
- GitHub PAT: Stored in GOPASS (`gopass show github/yukilabs-core`)
