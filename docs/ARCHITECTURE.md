# Architecture — Sakshi Gupta Portfolio

**Last updated:** 2026-05-06

---

## 1. Tech Stack

| Technology | Why |
|---|---|
| **Astro** | Static-first — renders to zero-JS HTML, interactive bits opt in via React islands |
| **Tailwind CSS v4** | Utility-first styling with no component library overhead; small component surface doesn't justify a UI kit |
| **Framer Motion** | Declarative scroll reveals, staggered entrances, hover states — runs only inside React islands |
| **React** | Required by Framer Motion; used exclusively for animated islands, not for layout or content |
| **TypeScript** | Type-safe content schemas and component props; catches errors at build time |
| **Vercel** | Static adapter, edge CDN, preview deploys on push, zero config for Astro |

**Not used:** No backend, no database, no API routes, no auth, no CMS, no shadcn/ui.

---

## 2. Project Structure

```
portfolio/
├── docs/
│   ├── PRD.md
│   ├── ARCHITECTURE.md
│   └── content/                    # reference docs — not consumed by build
│       ├── site.md
│       ├── gbot-x.md
│       ├── dukaan.md
│       └── vymo.md
│
├── src/
│   ├── content/
│   │   ├── config.ts               # content collection schemas
│   │   └── projects/
│   │       ├── gbot-x.md           # frontmatter + markdown body
│   │       ├── dukaan.md
│   │       └── vymo.md
│   │
│   ├── data/
│   │   └── site.ts                 # static config: bio, links, experience, socials
│   │
│   ├── layouts/
│   │   ├── BaseLayout.astro        # <html>, <head>, meta, fonts, global styles
│   │   └── CaseStudyLayout.astro   # shared case study page shell
│   │
│   ├── pages/
│   │   ├── index.astro             # home — single-page scroll
│   │   └── work/
│   │       └── [slug].astro        # dynamic route → one page per project
│   │
│   ├── components/
│   │   ├── Nav.astro
│   │   ├── Hero.astro
│   │   ├── ProjectCard.astro
│   │   ├── ProjectGrid.astro
│   │   ├── Experience.astro
│   │   ├── Contact.astro
│   │   ├── Footer.astro
│   │   ├── LoomEmbed.astro
│   │   ├── SectionHeading.astro
│   │   └── motion/                 # React islands — only these ship JS
│   │       ├── FadeIn.tsx
│   │       ├── StaggerChildren.tsx
│   │       ├── HoverCard.tsx
│   │       └── PageTransition.tsx
│   │
│   └── styles/
│       └── global.css              # Tailwind directives, @font-face, CSS custom properties
│
├── public/
│   ├── fonts/                      # self-hosted font files (woff2)
│   ├── images/
│   │   ├── projects/               # case study covers + inline visuals
│   │   └── og/                     # open graph images (home + 3 case studies)
│   └── favicon.svg
│
├── astro.config.mjs
├── tailwind.config.ts
├── tsconfig.json
└── package.json
```

---

## 3. Pages & Routing

4 static pages. All pre-rendered at build time. No SSR.

| Route | File | What it does |
|---|---|---|
| `/` | `pages/index.astro` | Single-page scroll: Hero → Projects → Experience → Visual Design → Contact → Footer |
| `/work/gbot-x` | `pages/work/[slug].astro` | GBOT-X case study |
| `/work/dukaan` | `pages/work/[slug].astro` | Dukaan case study |
| `/work/vymo` | `pages/work/[slug].astro` | Vymo case study |

`[slug].astro` uses `getStaticPaths()` to generate one page per entry in the `projects` content collection. Navigation between home and case studies is standard `<a>` links — no client-side router.

---

## 4. Component Breakdown

### Astro Components (zero JS)

| Component | Purpose | Props |
|---|---|---|
| `Nav.astro` | Fixed top nav. Logo/name left, section links right. Smooth scroll anchors on home, regular links on case study pages. | `currentPage: string` |
| `Hero.astro` | Above-the-fold intro. Name, role, philosophy quote, resume button. | None — reads from `site.ts` |
| `ProjectCard.astro` | Single project card. Cover image, title, one-line description, type badge. Links to `/work/[slug]`. | `title: string`, `subtitle: string`, `type: string`, `slug: string`, `coverImage: string` |
| `ProjectGrid.astro` | Lays out 3 `ProjectCard` components. Fetches from content collection, sorts by `order`. | None — fetches internally |
| `Experience.astro` | Work history. Company, role, period, location. Minimal timeline layout. | None — reads from `site.ts` |
| `Contact.astro` | CTA text, Calendly button (primary), email/phone/social links. | None — reads from `site.ts` |
| `Footer.astro` | Closing message. Back-to-top link. | None |
| `LoomEmbed.astro` | Responsive 16:9 iframe wrapper for Loom videos. Lazy loaded. | `url: string`, `title: string` |
| `SectionHeading.astro` | Consistent section title styling. Optional subtitle. | `title: string`, `subtitle?: string` |

### React Islands (Framer Motion — ships JS)

| Component | Purpose | Props | Hydration |
|---|---|---|---|
| `FadeIn.tsx` | Wraps any content. Fades + slides up when scrolled into view. | `children`, `direction?: 'up' \| 'down' \| 'left' \| 'right'`, `delay?: number`, `duration?: number` | `client:visible` |
| `StaggerChildren.tsx` | Wraps a list/grid. Children animate in sequentially with configurable stagger. | `children`, `stagger?: number`, `delay?: number` | `client:visible` |
| `HoverCard.tsx` | Wraps project cards. Adds scale + shadow + cursor effect on hover. | `children`, `className?: string` | `client:load` |
| `PageTransition.tsx` | Wraps page content in `CaseStudyLayout`. Fade-in on mount. | `children` | `client:load` |

**Hydration rules:**
- `client:visible` — default. Hydrates when element enters viewport. Used for below-the-fold content.
- `client:load` — only for above-the-fold interactive elements (hero cards, page transitions).

---

## 5. Content Strategy

### Content Collection — Projects

Case studies are markdown files in `src/content/projects/`. Frontmatter holds structured metadata, the body holds the full case study narrative.

```ts
// src/content/config.ts
import { defineCollection, z } from 'astro:content';

const projects = defineCollection({
  type: 'content',
  schema: z.object({
    title: z.string(),                    // "GBOT-X: Gemach Trading Dashboard"
    subtitle: z.string(),                 // "A decentralized platform for traders"
    type: z.enum([
      'Work Project',
      'Personal Project',
      'Design Assignment',
    ]),
    order: z.number(),                    // display order on home (1, 2, 3)
    coverImage: z.string(),              // path relative to public/images/projects/
    overview: z.string(),                // one-paragraph summary for cards
    role: z.string(),                    // "Solo Designer, ideation to execution..."
    loom: z.array(z.object({
      label: z.string(),                 // "Walkthrough" or "Part 1: Process"
      url: z.string().url(),
    })),
    figma: z.string().url().optional(),
    notionSource: z.string().url().optional(),
  }),
});

export const collections = { projects };
```

**Markdown body** contains the full case study content with standard headings (`## Problem Statement`, `## Research`, etc.). Rendered by Astro's built-in markdown pipeline inside `CaseStudyLayout.astro`. Tailwind's `@tailwindcss/typography` plugin styles the prose.

### Static Data — `src/data/site.ts`

Everything that isn't a case study: name, role, philosophy, experience history, social links, CTA copy. Imported directly by components. Single source of truth — change once, updates everywhere.

### Content Flow

```
docs/content/*.md  →  human reference (not in build)
        ↓ (manually synced)
src/content/projects/*.md  →  Astro content collection (build input)
src/data/site.ts           →  imported by components (build input)
```

---

## 6. Responsive Strategy

### Breakpoints

| Name | Width | Target |
|---|---|---|
| `sm` | 640px | Large phones (landscape) |
| `md` | 768px | Tablets |
| `lg` | 1024px | Small laptops |
| `xl` | 1280px | Desktops |

Design is mobile-first. Base styles target phones, breakpoints layer on larger layouts.

### What Changes

| Element | Mobile (< 768px) | Tablet (768px–1023px) | Desktop (1024px+) |
|---|---|---|---|
| **Nav** | Hamburger menu or minimal (name + CTA button only) | Full horizontal links | Full horizontal links |
| **Hero** | Stacked vertically. Full-width text. | Stacked, wider measure | Side-by-side or centered with max-width |
| **Project cards** | Single column, stacked | 2-column grid | 3-column grid or large single-column feature cards |
| **Case study body** | Full-width prose, small images | Centered column with margin | Centered ~720px content column, images can break out wider |
| **Experience** | Stacked cards | 2-column | Inline timeline |
| **Contact** | Stacked CTA + links | Side-by-side | Side-by-side with more spacing |
| **Typography** | Base sizes (16px body) | Slight scale-up | Full scale (18px body, larger headings) |
| **Spacing** | Compact section padding (48–64px) | Medium (80–96px) | Generous (96–128px) |
| **Hover states** | Replaced with tap/active states | Active on devices with hover | Full hover effects |

### Type Scale

```
Mobile                    Desktop
h1:  36px / 2.25rem  →   60px / 3.75rem
h2:  28px / 1.75rem  →   42px / 2.625rem
h3:  22px / 1.375rem →   28px / 1.75rem
body: 16px / 1rem    →   18px / 1.125rem
small: 14px / 0.875rem → 14px / 0.875rem
```

Scaled via Tailwind's responsive prefixes (`text-4xl lg:text-6xl`), not CSS clamp — keeps breakpoint behavior predictable.

---

## 7. Animation Plan

All animations use Framer Motion inside React islands. Every animation respects `prefers-reduced-motion` — reduced motion users get instant rendering with no movement.

### Home Page

| Element | Animation | Trigger | Duration | Details |
|---|---|---|---|---|
| Hero text | Staggered fade-up | Page load | 400ms per item, 100ms stagger | Name → role → philosophy → resume button, sequentially |
| Section headings | Fade-up | Scroll into view | 500ms | Each heading enters as user scrolls to it |
| Project cards | Staggered fade-up | Scroll into view | 400ms per card, 150ms stagger | Cards 1→2→3 enter sequentially |
| Project card hover | Scale up (1.02) + shadow lift | Mouse enter | 200ms | Subtle — just enough to signal interactivity. No effect on touch. |
| Experience items | Staggered fade-up | Scroll into view | 400ms, 100ms stagger | Each job entry appears in sequence |
| Contact section | Fade-up | Scroll into view | 500ms | CTA and links enter together |

### Case Study Pages

| Element | Animation | Trigger | Duration | Details |
|---|---|---|---|---|
| Page content | Fade-in | Page mount | 300ms | Smooth entrance, no slide — keeps reading position clear |
| Section blocks | Fade-up | Scroll into view | 500ms | Each case study section (Problem, Research, etc.) reveals on scroll |
| Images | Fade-in + slight scale (0.98 → 1) | Scroll into view | 600ms | Slightly slower — images deserve a moment |
| Loom embeds | Fade-in | Scroll into view | 400ms | Thumbnail visible immediately, iframe loads lazy |

### Motion Constraints

- **UI feedback** (hover, press): max 200ms
- **Scroll reveals**: 400–600ms
- **Page transitions**: 300ms
- **Stagger delay**: 100–150ms between items
- **Easing**: `[0.25, 0.1, 0.25, 1]` (ease-out-quad) for entrances, `spring` for hover scale
- **Mobile**: No hover animations. Scroll reveals stay but with shorter durations (300ms).
- **`prefers-reduced-motion`**: All motion components check this. When enabled, elements render in their final state with `opacity: 1` and no transform — zero animation.

### Implementation Pattern

```tsx
// src/components/motion/FadeIn.tsx
'use client';
import { motion, useReducedMotion } from 'framer-motion';
import type { ReactNode } from 'react';

interface Props {
  children: ReactNode;
  direction?: 'up' | 'down' | 'left' | 'right';
  delay?: number;
  duration?: number;
}

const offsets = {
  up: { y: 24 },
  down: { y: -24 },
  left: { x: 24 },
  right: { x: -24 },
};

export default function FadeIn({
  children,
  direction = 'up',
  delay = 0,
  duration = 0.5,
}: Props) {
  const reduced = useReducedMotion();

  if (reduced) return <>{children}</>;

  return (
    <motion.div
      initial={{ opacity: 0, ...offsets[direction] }}
      whileInView={{ opacity: 1, x: 0, y: 0 }}
      viewport={{ once: true, margin: '-50px' }}
      transition={{ duration, delay, ease: [0.25, 0.1, 0.25, 1] }}
    >
      {children}
    </motion.div>
  );
}
```

```astro
---
// Usage in Astro
import FadeIn from '../components/motion/FadeIn';
import SectionHeading from '../components/SectionHeading.astro';
---

<FadeIn client:visible>
  <SectionHeading title="Featured Work" />
</FadeIn>
```
