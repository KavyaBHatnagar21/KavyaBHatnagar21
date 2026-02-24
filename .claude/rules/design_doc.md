# Kavya Bhatnagar — Portfolio Website Design System

### Freelancer Handoff Documentation

> **Read this before touching anything.**
> This document explains every design decision made on this website — not just the values, but the _reasons_ behind them. If you change something without understanding why it exists, you will break the coherence of the site. When in doubt, do less, not more.

---

## 1. The Design Philosophy

This website is built around a single idea: **restraint communicates confidence.**

The client, Kavya, is a Shopify and ecommerce designer positioning herself as a thoughtful expert — not a loud agency, not a cheap freelancer. The design reflects that. It is quiet, editorial, and precise. It does not try to impress with flashiness. It impresses through clarity and taste.

**The aesthetic reference point** is a high-quality editorial publication — think a thoughtful design magazine, or the website of a respected independent architect. Clean, warm, typographically strong, with generous spacing and a muted palette.

**What this site is not:**

- It is not a portfolio showcase that screams "look at my work"
- It is not an agency site with bold gradients, hero animations, and aggressive CTAs
- It is not a generic Squarespace template with stock photos and blue buttons

Every decision — spacing, font weight, color, animation speed — has been made to reinforce one feeling: _"This person knows exactly what she is doing."_

---

## 2. Colour System

All colours are defined as CSS custom properties (variables) at the `:root` level. **Never hardcode a hex value that corresponds to one of these variables.** Always use the variable. Font families are also defined as variables for consistency.

```css
:root {
  --ink: #121212; /* Primary text, dark backgrounds, primary button — softer than pure black */
  --paper: #f5f3ef; /* Page background — warm off-white, NOT pure white */
  --paper-warm: #ece9e3; /* Slightly darker warm tone — work item backgrounds, placeholder fills */
  --sage: #8fb6d9; /* Brand accent — powder blue, used for labels, highlights, hover states */
  --sage-muted: #c9d9e6; /* Lighter blue — used on dark backgrounds only */
  --sage-pale: #e9f0f5; /* Very light blue tint — section backgrounds (testimonials) */
  --mid: #7e8a94; /* Secondary text — cool grey, nav links, captions */
  --light: #cbd4db; /* Tertiary text — hints, decorative text, very low emphasis */
  --border: #d6dee4; /* All dividers, card borders, grid lines */
  --display: "Playfair Display", Georgia, serif;
  --body: "Instrument Sans", sans-serif;
}
```

### Colour Usage Rules

**`--ink`** is used for:

- All primary body text
- Section headings
- The primary `.btn` background
- The dark Services and CTA sections' background
- The nav logo

**`--paper`** is used for:

- The main page background — every light section sits on this
- Text that appears on dark (`--ink`) backgrounds (e.g. service card headings, CTA heading)
- The primary button text colour

**`--sage`** is the brand accent (powder blue) and should be used sparingly but consistently:

- Section eyebrow labels (`.lbl` class)
- The italic emphasis words in headings (`<em>` tags) on light backgrounds
- Hover states on links and buttons (e.g. `.btn:hover`, `.nc:hover`)
- The available status dot label
- CTA contact link icons

**`--sage-muted`** is the dark-background version of sage:

- Used only when sage appears on `--ink` backgrounds (Services section, CTA section)
- The italic `<em>` words in headings on dark backgrounds
- Service card link colour and icon colour on dark background
- Custom cursor expanded hover state

**`--sage-pale`** is a section background:

- Testimonials section
- Never use as text colour

**`--mid`** is for supporting text:

- Nav links (not active/CTA)
- Ghost button text
- Captions and secondary labels
- Insight section above-text and sub-text
- Footer links

**`--light`** is for very low-priority text:

- The vertical hero label
- The "Scroll to explore" hint
- Footer copyright
- Decorative/ambient text that should barely be noticed

**`--border`** is the only value to use for lines and dividers:

- `<hr>` elements
- Card borders
- Grid line separators
- Process step borders
- FAQ item separators
- Insight section dividers

### Hardcoded Colours on Dark Backgrounds

On `--ink` backgrounds (Services, CTA), these hardcoded values are used instead of variables because the variable palette doesn't cover dark-on-dark distinctions:

| Hex | Use |
| --- | --- |
| `#252523` | Divider lines, card borders on dark backgrounds |
| `#3a3a38` | Subtle borders (e.g. service card icon circle) |
| `#1a1f24` | Service card hover background (sage-tinted dark) |
| `#666` | Low-emphasis labels on dark |
| `#777` | Body text on dark, FAQ answers |
| `#888` | Process step body, FAQ sidebar text |
| `#999` | Service card body text, list items on dark |
| `#555` | List bullet/dash colour on dark |

### What You Must Never Do With Colour

- Do not introduce any new colours. If something feels like it needs a new colour, re-examine the design decision.
- Do not use pure `#000000` black or pure `#FFFFFF` white anywhere — **except** the custom cursor, which uses `#fff` with `mix-blend-mode: difference` to invert against any background.
- Do not increase the saturation of `--sage`. It is deliberately muted.

---

## 3. Typography

### Font Families

Two fonts are used. Only these two. Do not introduce a third. Both are available as CSS variables (`var(--display)` and `var(--body)`).

| Role               | Family           | Variable         | Google Fonts                                         |
| ------------------ | ---------------- | ---------------- | ---------------------------------------------------- |
| Display / Headings | Playfair Display | `var(--display)` | `Playfair+Display:ital,wght@0,400;0,500;1,400;1,500` |
| Body / UI          | Instrument Sans  | `var(--body)`    | `Instrument+Sans:ital,wght@0,300;0,400;0,500;1,300`  |

**Playfair Display** is a high-contrast serif with elegant italics. It is used for all major headings, the logo, large decorative numerals, and testimonial body text. It gives the site its editorial, authoritative quality.

**Instrument Sans** is a clean, geometric sans-serif. It is used for all body copy, navigation, buttons, labels, captions, and UI text. Its Light (300) weight is used extensively, which gives the body text an airy, modern feel that contrasts well with the heavy serif headings.

### Type Scale

This is not a rigid modular scale — sizes are chosen contextually. Here are all the sizes in use:

| Use                      | Size                        | Weight  | Family           | Notes                                          |
| ------------------------ | --------------------------- | ------- | ---------------- | ---------------------------------------------- |
| Hero H1                  | `clamp(52px, 7.5vw, 110px)` | 400     | Playfair Display | Fluid. Line height 1.0. Letter spacing -0.02em |
| Section H2 (large)       | `clamp(36px, 5vw, 64px)`    | 400     | Playfair Display | CTA section                                    |
| Section H2 (standard)    | `clamp(30px, 4vw, 48–52px)` | 400     | Playfair Display | Services, Process, Insight title, Work         |
| Section H2 (small)       | `clamp(26px, 3–3.5vw, 40–44px)` | 400 | Playfair Display | Testimonials, FAQ                              |
| Insight heading          | `clamp(20px, 2.2vw, 26px)`  | 400     | Playfair Display | Smaller heading for insight blocks             |
| Service card name        | `clamp(20px, 2vw, 26px)`    | 400     | Playfair Display | Fluid, on dark background                      |
| Nav logo                 | `22px`                       | 400     | Playfair Display | Italic                                         |
| Hero sub-paragraph       | `18px`                       | 300     | Instrument Sans  |                                                |
| Body / description       | `15px–16px`                  | 300     | Instrument Sans  | Line height 1.75–1.8                           |
| Supporting body          | `14px`                       | 300     | Instrument Sans  | Line height 1.75–1.85                          |
| Small/caption            | `13px`                       | 300–400 | Instrument Sans  | Nav links, process body, btn text              |
| Labels / eyebrows        | `14px`                       | 500     | Instrument Sans  | ALL CAPS, letter-spacing 0.14em. Class `.lbl`  |
| Micro text               | `11px–12px`                  | 300–500 | Instrument Sans  | Hero badge, footer copy, hero hints            |
| Decorative numerals      | `48px`                       | 400     | Playfair Display | Italic, colour `--border`                      |
| Large quote mark         | `56px`                       | 400     | Playfair Display | Italic, colour `--sage-muted`                  |

### The Italic Rule

Italics in Playfair Display are a deliberate design element used for emphasis in headings — specifically for the second line or the key phrase in every section heading. For example:

```
"Sales don't improve
until the store *does.*"

"Some things I've *worked on.*"

"Here are my *services*"

"When a store stops
supporting *sales?*"
```

This pattern — a plain first line, italic second line — is consistent across the entire site. **Every new heading you write should follow this pattern.** Do not break this rhythm. Do not use italics randomly. They carry specific meaning: the italic word is the payoff of the sentence.

In HTML this is always an `<em>` tag inside the heading. In light sections, `em` is coloured `--sage`. In dark sections (Services, CTA), `em` is coloured `--sage-muted`.

### Label / Eyebrow Pattern

Many sections use a small label above or alongside the heading. The utility class `.lbl` provides this:

```css
font-size: 14px;
font-weight: 500;
letter-spacing: 0.14em;
text-transform: uppercase;
color: var(--sage);
```

This is consistent across the site. Never use a label at a different colour. Never skip the letter-spacing. Some labels use contextual sizes (12px–14px) but always maintain the same weight, tracking, and uppercase treatment.

---

## 4. Spacing System

Spacing is not modular (no 8px grid). It is generous and contextual, biased toward breathing room. Here are the key values in use:

### Section Padding

- **Desktop:** `100px` top/bottom, `56px` left/right for all standard sections
- **CTA section:** `120px` top/bottom (more emphasis on the closing section)
- **Mobile (≤960px):** `24px` left/right horizontal padding

### Internal Section Spacing

- Between eyebrow label and H2: `20–24px`
- Between H2 and body paragraph: `20px`
- Between section header and content grid: `56–72px`
- Between body paragraphs: `28px`
- Insight blocks: `28px` vertical padding between blocks

### Grid Gaps

- Two-column grids (Insight, CTA): `64–80px` gap
- Three-column grids: `24px` gap (testimonials), `1px` gap (service cards — creates visible seams via background colour)
- Work grid: `2px` gap (intentional near-flush aesthetic)
- FAQ: `80px` gap between sticky left and content right

### Dividers

Horizontal rules (`<hr class="div">`) are used between sections to create clean breathing breaks. They use `margin: 0 56px` so they are inset from the page edges, not full-bleed. On mobile, margin collapses to `0`.

---

## 5. Layout Principles

### The Grid Philosophy

The site uses CSS Grid throughout. The layouts vary by section — not everything is equal columns.

Key layouts:

- **Insight section:** `1fr 1fr` — sticky heading left, content blocks right
- **Service cards:** `repeat(3, 1fr)` — three equal cards with `1px` gap (colour creates dividers)
- **Work grid:** `repeat(2, 1fr)` — equal halves, `2px` gap
- **Process steps:** `repeat(4, 1fr)` — equal quarters with visible border grid
- **Testimonials:** `repeat(3, 1fr)` — three equal cards
- **FAQ:** `280px 1fr` — sticky narrow left, wide right
- **CTA:** `1fr 1fr` — equal halves

### The Sticky Pattern

Section headings and ancillary content use `position: sticky; top: 100px` on desktop. This means as the user scrolls through long content, the heading stays visible. Currently used in:

- Insight section title (left column)
- FAQ section heading (left column)

### Section Background Rhythm

The sections alternate backgrounds to create visual separation without needing heavy borders:

| Section      | Background     |
| ------------ | -------------- |
| Hero         | `--paper`      |
| Insight      | `--paper`      |
| Services     | `--ink` (dark) |
| Work         | `--paper`      |
| Process      | `--paper`      |
| Testimonials | `--sage-pale`  |
| FAQ          | `--paper`      |
| CTA          | `--ink` (dark) |
| Footer       | `--paper`      |

This rhythm — light, light, **dark**, light, light, tinted, light, **dark**, light — creates a deliberate pacing. Do not add a new section without considering where it falls in this rhythm.

---

## 6. Component Specifications

### Navigation

- Fixed position, `z-index: 100`
- Background: `rgba(245,243,239,0.9)` with `backdrop-filter: blur(14px)` — frosted glass effect
- Logo (`.nl`): Playfair Display, italic, 22px, colour `--ink`
- Nav links (`.nr a`): Instrument Sans, 13px, weight 400, colour `--mid`, hover to `--ink`
- CTA link (`.nc`): weight 500, colour `--ink`, underlined with `border-bottom: 1px solid var(--ink)`, hover changes colour and border to `--sage`
- On scroll (`.sc` class added via JS when `scrollY > 30`): padding reduces from `22px 56px` to `15px 56px`, subtle `box-shadow: 0 1px 0 var(--border)` appears
- **Important:** The class name `.sc` is reserved for nav scroll state. Do not use `.sc` as a class name for any other component.
- **Do not add a hamburger menu unless specifically asked.** The responsive layout simplifies nav on mobile — if a mobile menu is needed, discuss with the client first.

### Primary Button (`.btn`)

```css
background: var(--ink);
color: var(--paper);
padding: 14px 28px;
font-family: var(--body);
font-size: 14px;
font-weight: 500;
letter-spacing: 0.05em;
border-radius: 0; /* Intentionally no border radius — sharp corners */
transition: background 0.25s, gap 0.25s;
```

- Hover: background changes to `--sage`
- Always includes a right-arrow SVG icon that translates 4px right on hover
- **No border radius.** This is deliberate. The sharp corners align with the editorial aesthetic.

### Ghost Button / Text Link (`.btn-ghost`)

```css
font-size: 14px;
font-weight: 400;
color: var(--mid);
gap: 8px; /* increases to 12px on hover */
transition: color 0.2s, gap 0.2s;
```

- Used for secondary actions ("See all work")
- No background, no border
- The gap animation (arrow slides slightly away) is the only hover effect

### Section Headings — The Two-Line Pattern

Every section heading follows this structure:

```html
<h2>
  First line in plain text<br />
  Second line with <em>italic payoff.</em>
</h2>
```

The `<br>` is intentional line breaking, not a paragraph break. Preserve it.

### Eyebrow Labels

```html
<p class="lbl">Label text in caps</p>
```

Always precedes the `<h2>`. Always in sage, always uppercase, always 14px/500/0.14em tracking.

### Insight Section (formerly "Observation")

The Observation section has been replaced with a more scannable Insight section:

- **Layout:** 2-column grid (`1fr 1fr`) — sticky heading left, content blocks right
- **Left column:** Section heading with `.insight-title` class, `position: sticky; top: 100px`
- **Right column:** 3 insight blocks separated by `<hr class="insight-hr">` dividers
- Each block contains: `.lbl` (label) → `.insight-above` (small question text) → `.insight-hd` (bold serif heading) → `.insight-sub` (supporting line)
- Block padding: `28px 0` (first child: no top padding, last child: no bottom padding)
- The profile photo has been removed from this section

### Work Grid Items

- Desktop: 2-column grid with `2px` gap (not `gap: 0` — the 2px creates visible seams)
- All items have uniform `4:3` aspect ratio
- Images use `object-fit: cover; object-position: top` to show the top part of screenshots
- Hover effect: caption fades in from bottom with `opacity: 0 → 1` and `translateY(6px → 0)`
- Caption overlay (`.wi-cap`): `position: absolute; inset: 0` with gradient `linear-gradient(transparent 40%, rgba(15, 15, 14, 0.58))`, flex column with `justify-content: flex-end`
- Placeholder text (before real images): Playfair Display italic, 13px, colour `--light`

### Service Cards (Dark Section)

The services section has been redesigned from a list layout to a **3-card grid**:

- **Layout:** `repeat(3, 1fr)` grid with `1px` gap, `background: #252523` on the grid container creates visible dividers
- **Cards (`.svc`):** `background: var(--ink)`, `padding: 40px 36px`, flex column layout
- **Hover:** background transitions to `#1a1f24` over `0.6s ease` — a subtle sage-tinted dark
- **Card structure:** icon circle (`.svc-icon`) → optional label (`.svc-lbl`) → heading (`.svc-name`) → "Best when" list → "You get" list → CTA link (`.svc-lnk`)
- **Icon circles:** `48px × 48px`, `border-radius: 50%`, `border: 1px solid #3a3a38`, colour `--sage-muted`
- **Lists (`.svc-list`):** dash-prefixed (`–`), `14px`, weight 300, colour `#999`
- **CTA links:** uppercase, `--sage-muted`, hover to `--paper`
- Mobile: cards stack to single column

### Process Steps

- 4-column grid enclosed in a single `1px solid --border` box
- Columns are separated by `border-right: 1px solid --border`
- Connector arrows (circular buttons) sit at `position: absolute; right: -11px; top: 40px` — they overlap the grid border precisely. Width/height is `22px` to straddle the 1px line.
- Decorative numbers: Playfair Display italic, `48px`, colour `--border` (very faint, decorative only)
- Mobile: collapses to 2-column grid

### Testimonial Cards

- Background: `--paper` on `--sage-pale` background — creates a lift effect
- Hover: `translateY(-4px)` with `box-shadow: 0 12px 40px rgba(0,0,0,0.06)` — subtle lift, no dramatic shadow
- Opening quote mark: Playfair Display italic, `56px`, colour `--sage-muted` — decorative, not structural
- Quote body: Playfair Display italic, `18px` — testimonials use the display font to feel human and warm

### FAQ Accordion

- Default: items closed, `max-height: 0`
- Open: `max-height: 400px` (CSS transition, not JS height calculation)
- The `+` icon rotates `45deg` to become `×` when open
- Only one item can be open at a time (JS function `tf()` closes others on open)
- Question text (`.fq`): Instrument Sans, `15px`, weight 500, hover to `--sage`
- Answer text (`.fa p`): Instrument Sans, `14px`, weight 300, colour `#777`

### Custom Cursor

The site uses a custom cursor — the native cursor is hidden (`cursor: none`). **The cursor is only active on devices with a fine pointer** (mouse/trackpad) — touch devices get the native cursor.

Both the CSS and JS are wrapped in `@media (pointer: fine)` / `matchMedia("(pointer:fine)")`.

- Default state: `8px × 8px` circle, `#fff` background, `mix-blend-mode: difference` — this inverts against any background, ensuring visibility on both light and dark sections
- Hover state (over links/buttons): expands to `30px × 30px`, colour `--sage-muted`, `mix-blend-mode: multiply`
- Movement uses a lerp (linear interpolation) animation at `0.10` factor for a smooth, floaty trailing effect
- **Do not remove this.** It is a deliberate part of the experience. If adding new interactive elements, ensure they trigger the `.on` class.

### Profile Photo

The profile photo uses a `<picture>` element to serve different images based on device:

```html
<picture>
  <source media="(max-width: 960px)" srcset="assets/images/profile.png" />
  <img src="assets/images/kavya.jpeg" alt="Kavya Bhatnagar" />
</picture>
```

- Desktop: `kavya.jpeg`
- Mobile: `profile.png`

---

## 7. Animation & Motion

### Core Principles

- All animations are **subtle and purposeful** — they should not be noticed as animations, only felt as the page feeling smooth
- No bouncing, no overshooting, no spinning
- Duration is short: `0.2s–0.7s`. Nothing longer than `0.7s` except the scroll reveal
- Easing: always `ease` — never `linear`, never `ease-in-out` for transitions (that's for animations)
- Exception: service card hover uses `0.6s ease` for a deliberately soft, slow background shift

### Hero Load Animations

Elements animate in sequentially on page load using CSS `animation` with staggered delays:

```
Available badge:     0.2s delay, 0.7s duration
H1 heading:          0.35s delay, 0.9s duration
Sub paragraph:       0.6s delay, 0.7s duration
CTA button wrap:     0.75s delay, 0.7s duration
Vertical side label: 1.2s delay, 1.0s duration (fade only, no translateY)
```

Animation keyframes:
- `fu` (fadeUp): `translateY(22px) → none` while fading in
- `fi` (fadeIn): `opacity: 0 → 1` (used for vertical label)
- `br` (blink): pulsing scale/opacity animation on the available dot, `2.5s ease-in-out infinite`

### Scroll Reveal

All major content blocks use the `.reveal` class with IntersectionObserver:

- Default: `opacity: 0; transform: translateY(26px)`
- Triggered (`.in` class added): `opacity: 1; transform: none`
- Duration: `0.7s ease`
- Stagger classes: `.rd1` (0.1s), `.rd2` (0.2s), `.rd3` (0.3s), `.rd4` (0.4s)
- Threshold: `0.1` — triggers when 10% of element is visible
- One-time: observer unobserves after first reveal

**Apply `.reveal` to every new content section or significant element you add.**

### Hover Transitions

Standard hover transition durations:

- Colour changes: `0.2s`
- Background changes: `0.25s`
- Service card background: `0.6s ease` (deliberately slower for softness)
- Transform (button arrow, card lift): `0.25s`
- FAQ accordion: `0.4s ease` (slightly slower for feel)
- Nav padding on scroll: `0.35s`
- Cursor size/colour: `0.25s`

---

## 8. Responsive Behaviour

Breakpoint: `max-width: 960px` — there is one breakpoint only.

### What Changes at Mobile

- All horizontal padding drops from `56px` to `24px`
- All multi-column grids collapse to single column
- Exception: process steps go `4 → 2` columns (not single)
- The vertical hero label (`writing-mode: vertical-rl`) is hidden on mobile
- Nav padding reduces to `16px 24px`
- Sticky positioning is removed from insight title and FAQ heading
- Service cards stack to single column
- Insight block padding reduces to `24px 0`, heading to `20px`
- CTA grid collapses to single column with `48px` gap
- Footer collapses to single column, centered
- Custom cursor is completely disabled on touch devices via `@media (pointer: fine)`

### Mobile Philosophy

The mobile layout is functional and clean, not elaborate. The priority order of information is preserved — headings first, then body, then actions. Do not add new mobile-specific layouts without considering the single-breakpoint philosophy.

---

## 9. Page Sections Reference

A complete map of every section in order:

| Order | Section       | Class/ID                | Background    | Notes                                   |
| ----- | ------------- | ----------------------- | ------------- | --------------------------------------- |
| 1     | Navigation    | `nav#nav`               | Frosted paper | Fixed, z-index 100                      |
| 2     | Hero          | `section.hero`          | `--paper`     | Full viewport height                    |
| —     | Divider       | `hr.div`                | —             | Inset 56px                              |
| 3     | Insight       | `section.insight`       | `--paper`     | 2-col grid, sticky heading + 3 blocks   |
| 4     | Services      | `section.svcs#services` | `--ink`       | Dark section, 3-card grid               |
| —     | Divider       | `hr.div`                | —             | Inset 56px                              |
| 5     | Work          | `section.work#work`     | `--paper`     | 2-col work grid                         |
| 6     | Process       | `section.proc`          | `--paper`     | 4-col step grid                         |
| 7     | About         | `section.about`         | `--paper`     | 2-col: sticky photo left, bio text right|
| 8     | Testimonials  | `section.testi`         | `--sage-pale` | 3-col cards                             |
| 9     | FAQ           | `section.faq`           | `--paper`     | 2-col sticky layout                     |
| 10    | CTA / Contact | `section.cta#contact`   | `--ink`       | Dark section                            |
| 11    | Footer        | `footer`                | `--paper`     | 3-col flex                              |

---

## 10. Writing Style & Voice

Design and copy are inseparable on this site. If you are writing any new content (section labels, button text, placeholder copy), follow these rules:

**Tone:** Clear, direct, calm. Not salesy. Not hype. Not agency-speak.

**What to write:**

- Declarative statements, not questions
- Short to medium sentences
- Observations, not claims
- Plain English — no jargon

**What to never write:**

- "Are you struggling with...?" — No questions that assume pain
- "World-class", "cutting-edge", "holistic", "synergy" — No buzzwords
- "Let's grow together!" — No forced enthusiasm
- "I help brands scale their online presence" — No vague mission statements

**Heading pattern:** The heading always starts with a plain observation or statement, and the italic second line is the emotional or conceptual payoff. Never reverse this order.

**Labels:** Short, 2–5 words, descriptive of what the section is — not clever or cryptic. Examples: `The real issue`, `Why effort isn't working`, `How I work`, `From clients`.

---

## 11. Things You Must Not Change

These are protected decisions. Do not alter them without explicit discussion with the client:

1. **The font pairing.** Playfair Display + Instrument Sans is the identity of this site.
2. **The colour palette.** No new colours. No more saturated versions of existing colours.
3. **The italic heading pattern.** Every H2 must have the plain/italic two-line structure.
4. **The custom cursor.** It is part of the experience. It must remain disabled on touch devices.
5. **The no-border-radius rule on buttons.** Sharp corners are intentional.
6. **The `--paper` background.** Do not use pure white (`#fff`) for any background (cursor is the only exception).
7. **The section rhythm (light/dark alternation).** Do not put two dark sections or two tinted sections next to each other.
8. **The `2px` work grid gap.** It looks like a mistake but it is not.
9. **The label/eyebrow style.** 14px, 500 weight, 0.14em tracking, uppercase, sage — always.
10. **The animation timing.** Do not add faster snappy animations or slower cinematic ones. Stay in the `0.2–0.7s` range (service card hover at `0.6s` is the upper bound).
11. **The `.sc` class name.** Reserved for nav scroll state — do not reuse for any other component.

---

## 12. Adding New Sections

When adding a new section, follow this checklist:

- [ ] Does it follow the section background rhythm? (Check the table in Section 9)
- [ ] Does it use `padding: 100px 56px`?
- [ ] Does the heading follow the italic payoff pattern?
- [ ] Are all colours from the established palette?
- [ ] Are all text sizes from the established type scale?
- [ ] Have `.reveal` and appropriate `.rd1/.rd2/.rd3` delay classes been applied?
- [ ] Does it collapse correctly at `max-width: 960px`?
- [ ] If it has interactive elements, do they trigger the cursor `.on` class?
- [ ] On dark backgrounds, are you using the hardcoded dark-section colours (see Section 2)?

---

## 13. File Structure Notes

The current site is a single HTML file with embedded CSS and JS. When this is moved to a proper build system, the CSS variables in `:root` should be the first thing extracted into a shared design tokens file. The component structure maps cleanly to the sections listed in Section 9.

---

## 14. Changelog

Decisions made after the original freelancer handoff:

- **Colour palette shifted from green to powder blue.** All `--sage` values changed from muted green (#6f7f73) to powder blue (#8fb6d9). The entire palette was adjusted to align — `--sage-muted`, `--sage-pale`, `--mid`, `--light`, and `--border` all shifted to cool-toned equivalents.
- **`--ink` changed** from `#0f0f0e` to `#121212` (softer).
- **Observation section replaced with Insight section.** Long-form paragraphs replaced with 3 scannable insight blocks (label → question → bold statement → supporting line). Layout changed from 3-column (label/text/photo) to 2-column (sticky heading/blocks). Profile photo removed from this section.
- **Services section redesigned.** Changed from numbered list rows to 3-card grid with icons, "Best when" / "You get" lists, and soft hover effect. Old `.sr-*` classes replaced with `.svc-*` classes.
- **Services moved before Work** in the section order. Previously: Insight → Work → Services. Now: Insight → Services → Work.
- **Work grid items are now uniform.** First item no longer spans 2 columns — all items are `4:3` aspect ratio in a standard `2x2` grid.
- **Custom cursor updated.** Background changed to `#fff` with `mix-blend-mode: difference` (inverts against any background). Previously was `var(--ink)` with `mix-blend-mode: multiply`. Lerp factor reduced from `0.16` to `0.10` for a softer trail.
- **Custom cursor disabled on touch devices.** CSS and JS wrapped in `@media (pointer: fine)` / `matchMedia("(pointer:fine)")`.
- **Profile photo uses `<picture>` element.** Different images served for desktop (kavya.jpeg) and mobile (profile.png).
- **Nav logo size** changed from 19px to 22px.
- **Button font size** changed from 13px to 14px.
- **Label font size** changed from 11px to 14px.
- **Font family variables** (`--display`, `--body`) added to `:root` for convenience.
- **About section added** between Process and Testimonials. 2-column layout (`340px 1fr`) with sticky photo + caption on left, bio text on right. Uses `<picture>` element for responsive photo. Mobile: single column with centered circle photo.

---

_This document was last updated to reflect the current state of the codebase. Any future decisions that deviate from this document should be recorded in the Changelog (Section 14) so future contributors remain aligned._
