# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Personal portfolio and blog site for jcaldea.dev. Built with Astro 6, Tailwind CSS 4, and MDX. Site language is Spanish (`lang="es"`). Deployed to Vercel.

## Commands

- `npm run dev` — dev server at localhost:4321
- `npm run build` — production build to `./dist/`
- `npm run preview` — preview production build locally

No test runner or linter is configured.

## Architecture

**Layouts:**
- `Base.astro` — main layout wrapping all pages (Navbar, Footer, BgBlobs, CustomCursor, SEO). Imports `global.css` via `<style is:global>`.
- `Docs.astro` — layout for project documentation pages (sidebar nav, TOC, header with badges). Used by `/projects/taghound` and `/projects/packwatch`.

**Content collection:**
- Blog posts live in `src/content/blog/` as `.mdx` files.
- Schema defined in `src/content.config.ts`: `title`, `description`, `date`, `tags`, `draft` (boolean, defaults false).
- Posts with `draft: true` are filtered out in all queries.
- Dynamic route at `src/pages/blog/[slug].astro` renders posts using `post.id` as slug.

**Styling:**
- Tailwind CSS 4 via Vite plugin (not Astro integration). Config is in `global.css` using `@theme` directive for custom design tokens.
- Design tokens: dark background (`#0c0f18`), cyan accent (`#00d4ff`), violet secondary (`#7c5cfc`).
- Fonts: Syne (headings/body), Space Mono (code/labels) — loaded from Google Fonts.
- Most component styling uses scoped `<style>` blocks with CSS custom properties, not Tailwind utility classes.

**Code highlighting:** Shiki with `github-dark-default` theme, configured in `astro.config.mjs`.

## Key Conventions

- Dates formatted with `es-CL` locale.
- Project doc pages (`/projects/*`) use the `Docs` layout and pass sidebar/toc data as props.
- Custom MDX components for docs live in `src/components/docs/` (Terminal, InstallTabs, FlagsTable).
- Node.js >= 22.12.0 required (see `engines` in package.json).
