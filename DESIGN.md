# Design System — V1 Editorial Studio

Design language for sakshigupta.in. Minimal, typographic, editorial.

---

## Tokens

### Color

| Token        | Variable     | Hex       | Usage                                      |
|-------------|-------------|-----------|---------------------------------------------|
| Background  | `--bg`      | `#FFFFFF` | Page background                             |
| Ink         | `--ink`     | `#0E0E10` | Primary text, headings, section dividers    |
| Ink 2       | `--ink-2`   | `#3C3C42` | Body text, descriptions                     |
| Muted       | `--muted`   | `#8A8A92` | Kickers, labels, meta text, status text     |
| Muted 2     | `--muted-2` | `#B5B5BB` | Arrows (resting), lowest-priority text      |
| Line        | `--line`    | `#ECECEE` | Borders, dividers, underlines               |
| Line 2      | `--line-2`  | `#F4F4F6` | Thumbnail backgrounds, subtle fills         |
| Accent      | `--accent`  | `#006FC9` | Links (hover), CTA highlights, active state |
| Success     | —           | `#00A36C` | Status dot ("Open to work")                 |

### Typography

| Role              | Family          | Size      | Weight | Tracking     | Transform  |
|-------------------|-----------------|-----------|--------|-------------|------------|
| Body              | Geist           | 15px      | 400    | 0            | —          |
| Hero heading      | Geist           | 26px      | 500    | -0.015em     | —          |
| Hero body         | Geist           | 15.5px    | 400    | 0            | —          |
| Section label     | Geist           | 13px      | 500    | 0.1em        | uppercase  |
| Work title        | Geist           | 22px      | 500    | -0.015em     | —          |
| Work description  | Geist           | 14.5px    | 400    | 0            | —          |
| Experiment title  | Geist           | 15.5px    | 500    | 0            | —          |
| Experiment desc   | Geist           | 13.5px    | 400    | 0            | —          |
| Kicker / meta     | Geist Mono      | 11px      | 400    | 0.1em        | uppercase  |
| Count badge       | Geist Mono      | 10.5px    | 400    | 0.1em        | uppercase  |
| Stack label       | Geist Mono      | 10px      | 400    | 0.08em       | uppercase  |
| Nav links         | Geist           | 14.5px    | 400    | 0            | —          |
| Footer heading    | Geist           | clamp(26–34px) | 500 | -0.02em  | —          |
| Email CTA         | Geist           | clamp(22–28px) | 500 | -0.02em  | —          |
| Footer meta       | Geist Mono      | 11px      | 400    | 0.08em       | uppercase  |

**Font stack:** `'Geist', system-ui, sans-serif` / `'Geist Mono', monospace`

**Line heights:** Body 1.55 · Hero heading 1.25 · Hero body 1.6 · Work title 1.2 · Work desc 1.55 · Exp desc 1.4 · Footer heading 1.2

**Rendering:** `-webkit-font-smoothing: antialiased` · `font-feature-settings: 'ss01'`

### Spacing

| Token              | Value   | Usage                            |
|-------------------|---------|----------------------------------|
| Page max-width    | 760px   | `.wrap` container                |
| Page padding      | 28px    | Horizontal gutters               |
| Topbar top        | 28px    | Top padding                      |
| Hero top          | 88px    | Above hero                       |
| Hero bottom       | 72px    | Below hero                       |
| Section padding   | 48px    | Vertical section spacing         |
| Section head mb   | 8px     | Below section header border      |
| Section head pb   | 14px    | Above section header border      |
| Work card gap     | 56px    | Between stacked work cards       |
| Thumb mb          | 24px    | Below thumbnail, above content   |
| Meta mb           | 14px    | Below kicker row                 |
| Title mb          | 8px     | Below work title                 |
| Exp row padding   | 16px    | Vertical padding per row         |
| Footer top        | 88px    | Above footer                     |
| Footer bottom     | 56px    | Below footer                     |
| Footer mt         | 56px    | Margin above footer border       |
| Nav gap           | 18px    | Between nav links                |
| Social gap        | 18px    | Between social links             |

#### Mobile overrides (max-width: 600px)

| Token            | Value   |
|-----------------|---------|
| Hero top        | 56px    |
| Hero bottom     | 48px    |
| Hero h1 size    | 22px    |
| Section padding | 32px    |
| Work card gap   | 40px    |
| Work title size | 19px    |
| Footer top      | 56px    |
| Footer bottom   | 48px    |
| Exp grid        | `44px 1fr 18px` (stack label hidden) |

### Radius

| Element        | Value |
|---------------|-------|
| Thumbnail     | 8px   |
| Selection     | —     |

### Shadows

None. The design is flat with border-based hierarchy.

---

## Components

### Topbar
- Left: name (weight 500)
- Right: nav links (muted) + CTA link (ink, with mono arrow `↗`)
- CTA arrow transitions: `translate(2px, -2px)` on hover, color to accent

### Status badge
- Green dot (7px) with pulse animation (`dot-pulse`, 2s infinite)
- Inline-flex with 8px gap, 13px muted text
- Pulse scales to 2.6x then fades

### Hero
- Status badge → h1 (26px/500) → body paragraphs (15.5px, ink-2)
- Inline links: ink color, 1px bottom border (line color), hover → accent
- Juspay link forced to accent color

### Section header
- Flex row: h2 (13px uppercase mono-spaced label) + count (10.5px mono)
- 1px bottom border in `--ink` (not line — this is intentional, strong divider)
- pb 14px, mb 8px

### Work card
- Thumbnail (16:10 aspect, CSS-only illustration, 8px radius)
- Meta row: kicker (mono 11px uppercase) + arrow (mono 16px accent)
- Title (22px/500) + description (14.5px ink-2, max-width 560px)
- Hover: title → accent, arrow → translateX(4px), thumb → translateY(-3px)
- Transition: `.35s cubic-bezier(.2,.8,.2,1)`

### Experiment row
- Grid: `56px 1fr auto 24px`
- Num (mono 10.5px) | title + desc | stack label (mono 10px) | arrow (mono 13px)
- Hover: padding-left 6px, title → accent, arrow → translateX(3px) + accent
- Bottom border: 1px `--line`

### Footer
- h3 with `.accent` span for colored word
- Large email link (clamp 22–28px) with underline + arrow
- Meta row: copyright (mono 11px) + social links

---

## Interaction patterns

| Element          | Property         | Duration | Easing                          |
|-----------------|-----------------|----------|---------------------------------|
| Nav link        | color            | 0.2s     | ease                            |
| CTA arrow       | color, transform | 0.2s     | ease                            |
| Inline link     | color, border    | 0.2s     | ease                            |
| Work card       | transform        | 0.35s    | cubic-bezier(.2,.8,.2,1)        |
| Work title      | color            | 0.2s     | ease                            |
| Work arrow      | transform        | 0.25s    | cubic-bezier(.2,.8,.2,1)        |
| Experiment row  | padding          | 0.2s     | ease                            |
| Experiment arrow| color, transform | 0.2s     | ease                            |
| Email link      | color, border    | 0.25s    | ease                            |
| Email arrow     | transform, color | 0.25s    | cubic-bezier(.2,.8,.2,1)        |
| Status dot      | scale, opacity   | 2s       | cubic-bezier(0.4, 0, 0.6, 1)   |

---

## Principles

1. **Typography does the work.** No decorative elements. Hierarchy comes from size, weight, and color contrast alone.
2. **Mono for metadata.** Geist Mono is reserved for kickers, counts, labels, arrows — never for body text.
3. **Accent is earned.** Blue appears only on hover states, active links, and the Juspay highlight. Everything else is neutral.
4. **Flat, not empty.** No shadows, no gradients on UI. Depth comes from spacing and the single strong section divider (`--ink` border).
5. **Calm motion.** Transitions are short (0.2–0.35s) with soft cubic-bezier curves. Nothing bounces or overshoots.
6. **Content-first thumbnails.** 16:10 aspect, CSS-only abstract art as placeholders — replace with real imagery.
