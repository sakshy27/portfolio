# CLAUDE.md

## Project
Personal portfolio site for Sakshi Gupta, a product designer at Juspay. See [docs/PRD.md](docs/PRD.md) and [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md) for full context.

## Stack
- Astro (static site generator)
- Tailwind CSS v4
- Framer Motion (via React islands)
- React (only for animated islands, not layout)
- TypeScript
- Vercel (hosting)

## Structure
```
astro-site/src/
├── components/       # Astro components (zero JS) + motion/ for React islands
├── layouts/          # Base.astro, CaseStudy.astro
├── pages/            # index.astro, work/dukaan.astro
├── styles/           # global.css, tokens.css
public/images/        # project covers, thumbnails
docs/                 # PRD, architecture, reference content
```

## Conventions
- Use Tailwind utility classes — no custom CSS files
- Use Framer Motion for all animations
- All content comes from static data files (no hardcoded strings in components)
- Follow the V1 Editorial Studio design system (Geist + Geist Mono, 760px max-width `.wrap`)
- Do not output code diffs or large code blocks in text responses — just briefly describe what changed
- Respect `prefers-reduced-motion` in all animations

## Content
- All real content is sourced from docs/content/ (site.md, gbot-x.md, dukaan.md, vymo.md)
- No placeholder text — every string should be real

## Docs
- docs/content/ — sourced content for all pages
- docs/PRD.md — product requirements
- docs/ARCHITECTURE.md — technical architecture
