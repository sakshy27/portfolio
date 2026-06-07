# Product Requirements Document — Sakshi Gupta Portfolio

**Status:** Draft
**Last updated:** 2026-05-06

---

## 1. Purpose & Goals

This is a personal portfolio site for Sakshi Gupta, a product designer currently at Juspay with prior experience at Intentionally Designed Solutions.

**What this site needs to do:**

- Position Sakshi as a thoughtful, research-driven product designer — not just someone who makes things look good, but someone who digs into problems, talks to users, and makes deliberate design decisions.
- Showcase 3 case studies that demonstrate range: a client project (GBOT-X), a capstone project (Dukaan), and a design assignment (Vymo). Each shows a different context but the same rigorous process.
- Make it effortless for a hiring manager or potential client to reach out. Every visit should end with a clear next step.

**Primary conversion actions (in priority order):**

1. Book a call via Calendly
2. Send an email
3. Download/view resume
4. Connect on LinkedIn or Twitter

**Secondary goal:** Establish a distinct personal brand that stands out from template-based designer portfolios.

---

## 2. Target Audience

### Primary: Hiring managers & design leads

- Evaluating candidates for product design roles (full-time or freelance)
- Scanning portfolios quickly — they'll spend 30-90 seconds deciding whether to dig deeper
- Looking for: evidence of process, not just final screens. Can this person think? Can they articulate decisions?
- Red flags they're watching for: all-visual portfolios with no reasoning, generic case studies, no clear role description

### Secondary: Peers & design community

- Other designers, 10kdesigners cohort members, Twitter/LinkedIn connections
- Looking for inspiration, shared learning, or collaboration
- More likely to engage with visual design and creative sections

### Tertiary: Potential clients

- Startups or teams looking for a freelance product designer
- Need to quickly assess: domain flexibility, communication skills, ability to work independently
- The GBOT-X case study (solo designer, client work, unfamiliar domain) speaks directly to this audience

---

## 3. Content Sections

The site is a single-page scrolling experience with distinct sections. Each section has a job to do.

### 3.1 Hero

**Job:** Make an immediate impression. Communicate who Sakshi is and what she does in under 5 seconds.

**Content:**
- Name: "Hey, I'm Sakshi"
- Role: Product Designer, currently @ Juspay
- Design philosophy: "I believe that great design goes beyond interfaces, diving into the minute details makes the experience truly exceptional."
- Resume link (Google Drive)

**Feel:** Confident but warm. Not corporate, not overly casual. The greeting style ("Hey, I'm Sakshi") sets this tone.

### 3.2 Featured Work

**Job:** This is the core of the site. Show that Sakshi doesn't just design — she researches, reasons, and iterates. Each project card should pull the visitor in with enough context to make them want to read more.

**3 project cards, each showing:**
- Project title
- One-line description
- Project type label (Work Project / Personal Project / Design Assignment)
- Cover image/visual

**Project order (intentional):**

1. **GBOT-X: Gemach Trading Dashboard** — Leads with the strongest story: unfamiliar domain, solo designer, client work, shipped product. Shows adaptability.
2. **Dukaan Subscriptions** — Shows depth of research (user interviews, comparative analysis, payment logic, notification systems). The most comprehensive case study.
3. **Vymo: Sales Manager Dashboard** — Shows UX audit skills, structured thinking, and the ability to work within constraints of an existing product.

Each card links to a dedicated case study view (see 3.3).

### 3.3 Case Study Pages

**Job:** Prove the process. Each case study should read as a narrative — problem, research, reasoning, solution — not a dump of deliverables.

**Shared structure for all case studies:**

| Section | Purpose |
|---|---|
| Overview | What is this project, in one paragraph |
| Problem Statement | What's broken and why it matters |
| Role | What Sakshi specifically did |
| Research | How she built understanding (interviews, competitive analysis, domain research) |
| Key Insights | What she learned, in bullet form |
| Pain Points | User frustrations distilled |
| Design Decisions | The "why" behind choices — not just what was designed, but why it was designed that way |
| Solution / Final Design | Visual output with context |
| Video Walkthrough | Embedded Loom video for each project |

**Project-specific highlights to feature:**

- **GBOT-X:** Domain learning journey (crypto newbie to informed designer), multi buy/sell feature rationale, 5 user interviews
- **Dukaan:** Comparative analysis table (5 platforms), payment method decision tree (Autopay vs wallet vs advance), notification system mapping, RBI guideline consideration
- **Vymo:** UX audit of existing flow, HMW framing, tab-based redesign rationale, chat vs call assumption with validation plan, Figma file link

**Loom videos per project:**
- GBOT-X: 1 video
- Dukaan: 2 videos (Part 1: Process, Part 2: Design & Iterations)
- Vymo: 1 video

### 3.4 Work Experience

**Job:** Provide professional context. Brief and factual — the case studies do the heavy lifting.

**Content:**
- Product Designer @ Juspay — May 2025 - Present, Bengaluru
- Product Designer @ Intentionally Designed Solutions — Feb 2024 - May 2025, Remote

### 3.5 Visual Design / Creative Space

**Job:** Show range beyond product design. A lighter section that balances the research-heavy case studies.

**Content:** "Let's make this easy on your eyes — Check out my creative space." Links to visual/creative work.

### 3.6 Contact / Let's Connect

**Job:** Convert interest into action. No friction.

**Content:**
- CTA: "I'm open to full-time and freelance opportunities in product design. Hiring? Let's have a quick chat!"
- Calendly booking link (primary CTA)
- Email: sakshigupta9368@gmail.com
- Phone: +91-9368413389
- Twitter: @sakshi_026
- LinkedIn: sakshi-gupta-225a3020b

### 3.7 Footer

**Content:** "Thanks for making it till the end. Have a great day ahead :)"

Light, personal sign-off. Consistent with the warm tone established in the hero.

---

## 4. Visual Direction

**To be decided.** This section will be filled in after visual exploration.

Areas to define:
- Color palette
- Typography (heading + body pairing)
- Spacing and layout grid
- Image treatment for case study visuals
- Light/dark mode preference
- Overall aesthetic direction (minimal, editorial, expressive, etc.)

---

## 5. Interactions & Motion

**To be decided in detail.** This section captures the interaction principles — specific implementations will follow visual direction.

### Principles

- Motion should feel intentional, not decorative. Every animation should either guide attention or provide feedback.
- Nothing should block content. No loading screens that delay access to the work.
- Interactions should reinforce the "attention to detail" positioning from the design philosophy.

### Areas where motion matters

| Element | Interaction type | Purpose |
|---|---|---|
| Page load | Staggered entrance of hero elements | First impression — set the tone |
| Project cards | Hover state with visual feedback | Signal interactivity, invite click |
| Case study transitions | Smooth page/section transitions | Maintain flow while reading |
| Scroll-triggered reveals | Content fading/sliding in as user scrolls | Create rhythm, prevent wall-of-text feeling |
| CTAs (Calendly, email) | Hover/press feedback | Make contact actions feel responsive |
| Loom embeds | Inline embed or thumbnail with play state | Let visitors preview without navigating away |
| Navigation | Smooth scroll to sections | Keep orientation on single-page layout |

### Constraints

- All animations must respect `prefers-reduced-motion` — provide equivalent static experience
- No animation should exceed 400ms for UI feedback; scroll-triggered reveals can be up to 600ms
- Mobile: reduce or simplify animations that depend on hover states

---

## 6. What Makes This Stand Out

Most designer portfolios fall into two traps: either all visuals with no reasoning, or walls of text that read like school reports. This site needs to avoid both.

**The differentiators:**

1. **Process is the product.** The case studies don't just show final screens — they show the thinking. The GBOT-X case study starts with "I was a complete newbie in this crypto domain" and walks through how she got to a shipped product. That honesty and learning arc is rare and memorable.

2. **Decision-making on display.** The Dukaan case study includes a payment method decision tree, a notification system map, and a reference to RBI regulations. This isn't a student project — it reads like real product thinking with real constraints.

3. **Range without confusion.** Three projects, three contexts (client work, capstone, assignment), same structured approach. A hiring manager sees consistency of process across varied domains (crypto, e-commerce, enterprise SaaS).

4. **Validation mindset.** The Vymo case study explicitly calls out assumptions and proposes how she'd validate them with data. This signals maturity — she knows what she doesn't know.

5. **The site itself is a case study.** As a product designer's portfolio, the site's own design, interaction quality, and attention to detail is being evaluated. Every micro-interaction, every layout choice, every piece of copy is a demonstration of the work.
