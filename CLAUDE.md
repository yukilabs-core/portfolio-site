# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Purpose

**Portfolio hub** showcasing 5 interconnected engineering projects. Entry point at `/` displays project cards with brief descriptions & links to GitHub Projects. Each project (① through ⑤) gets its own page `/project-01/`, etc., and may fetch data from shared Supabase database or call the API Server (project②).

**Five Projects:**
1. 業務ログ可視化 (Business Log Visualization) — Astro dashboard + Supabase + Render API
2. API基盤 (API Foundation) — Express.js REST API with JWT, Swagger docs
3. 検索AI / Knowledge DB — Astro UI + pgvector search + Cloudflare Workers AI
4. 業務データ分析 (Data Analysis) — Python analysis → HTML report
5. 判断ログシステム (Decision Log) — Astro form + Supabase RLS

## Development Commands

| Command | Purpose |
|---------|---------|
| `npm run dev` | Start local dev server at `http://localhost:4321` (hot reload) |
| `npm run build` | Build production site to `./dist/` |
| `npm run preview` | Preview production build locally |

## Project Structure

- **`src/pages/`** — File-based routing. `index.astro` is the hub; `project-01/`, `project-02/`, etc. are subpages
- **`src/components/`** — Reusable components (add as projects grow)
- **`public/`** — Static assets (favicon, images)
- **`astro.config.mjs`** — Empty; may add integrations if interactive components needed

## Key Architecture Notes

**Multi-language (JP/EN):** Query param `?lang=jp` or `?lang=en` toggles language in `index.astro`. No i18n library needed yet.

**Data & API Integration:**
- Projects will gradually connect to **Supabase PostgreSQL** (already set up at babpqrypkqmivqujgeyy.supabase.co)
- API Server (project②) at **Render** provides unified REST API for projects ①③④⑤
- Session Pooler connection: `aws-1-ap-northeast-2.pooler.supabase.com:5432`

**Astro Notes:**
- Static HTML generation at build time
- `.astro` files use server-side rendering syntax (can fetch data in `---` frontmatter)
- Inline `<style>` blocks for component styles; no CSS framework yet

## Deployment & CI/CD

1. Push to `main` → GitHub Actions triggers Cloudflare Pages build
2. Cloudflare auto-builds `npm run build` and deploys `./dist/`
3. Site live at: https://yukilabs-core.pages.dev (or custom domain if configured)

Test locally with `npm run build && npm run preview` before pushing.

## Environment Variables (Future)

When projects integrate with Supabase/API:
- Add `.env` file (ignored by git): `SUPABASE_URL`, `SUPABASE_ANON_KEY`, `API_SERVER_URL`
- Never commit secrets; use `.env.example` for documentation
- In Astro, expose only public vars via `PUBLIC_` prefix (e.g., `PUBLIC_SUPABASE_URL`)

## Cloudflare Pages Integration

- **Auto-deploy:** Push to `main` → GitHub App triggers build
- **Build command:** `npm run build`
- **Build output:** `dist/`
- **Framework preset:** Astro (auto-detected)
- **Environment in dashboard:** Set vars under Pages > portfolio-site > Settings

## GitHub Setup

- Repository: `git@github.com:yukilabs-core/portfolio-site.git`
- GitHub Projects board: `yukilabs-core/projects/1` (overall backlog)
- Each project has its own sub-project (Projects 2-6 for projects①-⑤)
- Cloudflare Pages linked via GitHub App (auto-deploy on push)
