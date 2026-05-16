# Handoff: Sonarchy Landing Site

## Overview

A marketing landing page for **sonarchy.com**, plus matching restyled About / Privacy / Terms pages. The landing site lives at the apex domain and links out to **play.sonarchy.com** for the actual game. It introduces the product, animates the 6 game phases inside a CRT TV, and includes legal pages and footer attribution.

Built as four standalone HTML files using the existing Sonarchy SMPTE design system. Designed to be lifted into the **sonarchy-youtube** Next.js codebase as new App Router routes — replacing or sitting alongside the existing `/about`, `/privacy`, `/terms` pages — and a new public landing route.

---

## About these design files

The files in this bundle are **design references created in HTML** — high-fidelity prototypes showing intended look, copy, animation, and behavior, **not production code to copy directly**.

Your job is to **recreate these designs inside the sonarchy-youtube Next.js app** using the codebase's established patterns:
- Next.js App Router (`app/` directory)
- React function components with hooks
- The existing SMPTE design tokens already declared in `app/globals.css` (`--smpte-*` variables, `--charcoal-gray-*`, etc.)
- `framer-motion` for animations (already in use across `app/intro/page.tsx`, `app/splash-screen.tsx`, etc.)
- `next/image` for image components, `next/link` for navigation
- The existing `BottomNav` component pattern from `/about`, `/privacy`, `/terms` should NOT be applied to the **public landing/about/privacy/terms pages described here** — these are marketing pages accessed before login, not in-game routes.

Where the existing in-game routes (`app/about/page.tsx`, `app/privacy/page.tsx`, `app/terms/page.tsx`) already exist and serve in-game users, **keep them**. The pages in this bundle are intended for the **marketing site at sonarchy.com (apex)**, distinct from `play.sonarchy.com` (the app). If you're deploying both from the same Next.js app, route them differently — e.g., the marketing pages at `/`, `/about`, `/privacy`, `/terms` for unauthenticated visitors, and reuse the existing routes for in-game.

---

## Fidelity

**High-fidelity.** Pixel-perfect mockups with final colors, typography, spacing, copy, and animation timing. The developer should recreate the UI pixel-perfectly using the codebase's existing libraries and patterns.

---

## Pages

### 1. `landing.html` — Marketing landing page

**Route target:** `app/(marketing)/page.tsx` (or wherever you choose to host the apex domain marketing site).

**Layout (top to bottom):**

1. **Hero** (full viewport region, dark `#070707` superblack background, film-grain overlay)
   - Sonarchy logo SVG (`assets/brand/sonarchy-logo-lines.svg`) — the colored SMPTE rails are baked into the logo SVG itself; no extra stripes are needed.
   - Neon line waves background (`assets/brand/hero-neon-lines.svg`), faded in behind everything else, fixed at 200% width and centered.
   - CRT TV frame (`assets/brand/hero-tv-frame.svg`) at clamp(300px, 58vw, 480px) wide, aspect 380/360.
   - Casey (`assets/brand/hero-casey.svg`) and Walker (`assets/brand/hero-walker.svg`) peeking over the top edge of the TV, anchored at `bottom: calc(100% - 12px)` of the TV. Casey is on the left at 26% height rotated -4deg; Walker on the right at 32% height rotated 4deg.
   - **TV screen**: an animated 6-frame text cycler (see "TV animation" section below).
   - Tagline: "The music category party game where one speaker meets many controllers." in Inter 700, uppercase, 0.04em tracking, ~clamp(16px, 2.2vw, 22px).
   - Primary CTA button: `<a class="btn-play" href="https://play.sonarchy.com">Play now</a>` — magenta sticker with cyan offset shadow (see "Buttons" section).

2. **SMPTE bar divider** — 14px tall, 8 evenly-flexed bars in the SMPTE color order (white, yellow, cyan, green, magenta, red, blue, near-black) with 3px white stroke top + bottom.

3. **How It Works** section
   - Eyebrow label: "/ how it works /" in Inter 700, uppercase, cyan, 0.16em tracking.
   - Heading: "Press play." in Modak, clamp(40px, 9vw, 96px).
   - 3 step cards in a 1-column → 3-column grid (≥768px). Each step is rendered as a hanging classroom-projector mockup with:
     - Two "string" pseudo-elements (3px wide, 26px tall, rotated ±14deg) hanging from the top.
     - A chunky black control bar at the top 18% of the card with a metallic gradient inset and 4 colored dots (cyan/yellow/green/magenta).
     - A `#050507` screen below with a giant Modak step number (01/02/03) colored yellow/cyan/magenta per step, plus a kicker like "/ gather /", "/ pick /", "/ vote /".
     - Below the projector, a heading + paragraph.
   - Each card has a tiny tilt (-0.6deg, 0.4deg, -0.4deg).
   - CTA: another "Play now" button centered below.

4. **Another SMPTE divider.**

5. **Meet the Crew** section
   - Eyebrow: "/ meet the crew /"
   - Heading: "Six players. One still classified." in Modak.
   - 6 polaroid-style cards on a 1 → 2 → 3 column grid. Each card has:
     - Cream-white polaroid background, 2px border, 1px outer shadow, 6px/6px hard-offset SMPTE-color shadow (each card has a different shadow color), 18px/36px soft drop-shadow, slight rotation (-1.2 to 1.2 deg).
     - A dark CRT-style photo well containing the character SVG (`assets/characters/<name>.svg`) at 72% width.
     - A speech bubble badge in the top-right corner, rotated 6deg, with the character's catchphrase ("Pick it", "No peeking", "The warmth", "Crank it", "Let's go", "Coming soon").
     - Character name in Modak (clamp(36px, 4.4vw, 44px)) black on white, plus an italic blurb.
   - Card 6 ("Coming soon") is `.unrevealed`: a silhouette with SMPTE-bar gradient masked through it, name shown as `█████`.
   - CTA below.

6. **SMPTE divider.**

7. **Footer**
   - Two-column grid (1 col on mobile, 2 cols at ≥768px).
   - **Left:** Developed-by lockup. Eyebrow "Developed by", then 333 Games logo (`assets/brand/333Logo.svg`, inverted to white). Meta paragraph. Then an "About" block linking to about.html. Then a "Get in touch" block with `mailto:hello@sonarchy.com`.
   - **Right:** YouTube attribution. Uses the official light-variant "Developed with YouTube" SVG (`assets/brand/developed-with-youtube.svg`) at 28-36px tall, followed by the legal blurb: "Sonarchy uses the YouTube API Services. By playing, you agree to the [YouTube Terms of Service] and [Google Privacy Policy]." On ≥768px, this column gets a 1px left border + 64px left padding.
   - Bottom legal row: "© 2026 333 Games" on the left; Privacy Policy / Terms of Service links on the right, 12px uppercase 0.12em tracking.

### 2. `about.html` — About Sonarchy
Origin story page. Shared title bar pattern, single max-760px column. Body copy is in `pages.css` (see "Shared styles" below). Plain `landing.html` link at the back arrow.

### 3. `privacy.html` — Privacy Policy
Numbered legal sections (1–12) with effective date "12 May 2026". Content matches `app/privacy/page.tsx` from the github repo, restyled for desktop display.

### 4. `terms.html` — Terms of Service
Same shape as privacy, content matches `app/terms/page.tsx`.

---

## TV Animation (the headline interaction)

The `<div class="tv-screen">` inside the hero TV cycles through 6 frames. Each frame holds for **4400ms**, then a CRT glitch wipe (260ms, hue-rotate + jitter, `steps(4, end)`) covers the swap.

### Frame content

| # | Headline | Subtitle 1 | Subtitle 2 |
|---|---|---|---|
| 0 | Playlist clash · Party bash | — | — |
| 1 | Grab · your crew | — | — |
| 2 | Pick a category | Take turns choosing the theme | Road trip anthems · One hit wonders (yellow) |
| 3 | Find your track | Search and lock in your song | — |
| 4 | Skip or keep | Watch, listen & vote | — |
| 5 | Best taste wins | Vote. Rank. Reign. | — |

Headlines use VT323 in white, subtitles use VT323 in cyan, with a yellow accent variant for the categories example on frame 2.

### Per-letter entrance

On `is-active`, every visible character is wrapped in a `<span class="letter">` and runs **two parallel animations**:

1. **`letterIn`** (450ms, `cubic-bezier(.34,1.56,.64,1)`) — opacity 0→1 + translateY(0.5em)→0 with a slight overshoot (-0.08em → 0).
2. **`shadowCycle`** (1600ms, linear) — the letter's `text-shadow` cycles through SMPTE bar colors, then settles to soft white:
   - 0% → yellow glow
   - 16% → cyan glow
   - 33% → green glow
   - 50% → magenta glow
   - 66% → red glow
   - 82% → blue glow
   - 100% → soft white glow `0 0 6px rgba(255,255,255,0.45)`

Both animations are delayed by `var(--d)` per letter, stamped as `(idx * 38)ms` so letters cascade left-to-right.

On `is-leaving`, letters run `letterOut` (200ms ease-in) — opacity 1→0, translateY(0)→0.4em.

### Per-frame text sizing

Font size is set with **container queries** based on the screen cavity width, with per-frame overrides via custom properties:

```css
.tv-frame[data-frame="0"] { --tv-headline: 13cqw; }                          /* Playlist clash / Party bash */
.tv-frame[data-frame="1"] { --tv-headline: 17cqw; }                          /* Grab / your crew (shortest, biggest) */
.tv-frame[data-frame="2"] { --tv-headline: 9.5cqw; --tv-sub: 4.2cqw; }       /* Pick a category + 2 long subs */
.tv-frame[data-frame="3"] { --tv-headline: 12cqw; --tv-sub: 4.6cqw; }
.tv-frame[data-frame="4"] { --tv-headline: 14cqw; --tv-sub: 5.4cqw; }
.tv-frame[data-frame="5"] { --tv-headline: 12cqw; --tv-sub: 5cqw; }
```

The cycler respects `prefers-reduced-motion` — animation is disabled and letters appear instantly with the white glow.

### Suggested React implementation

This is a perfect fit for `framer-motion`'s `<AnimatePresence>` with the same per-character stagger pattern already used in `app/intro/page.tsx`. Keep the container query for sizing — or replace with `useMeasure()` + computed font-size if you prefer not to use CSS container queries.

---

## Hero entrance animation

When the page loads, hero elements animate in with this cadence (matches the intro flow from `play.sonarchy.com/intro` slide 1):

| Element | Delay | Animation |
|---|---|---|
| Logo | 0.05s | `heroSpringIn` — scale 0.5 → 1.08 → 0.97 → 1, fade in, 0.7s, `cubic-bezier(.34,1.56,.64,1)` |
| TV frame | 0.4s | `heroSpringIn`, 0.75s |
| Casey | 0.85s | `heroCaseyIn` — slides in from upper-left, ends rotated -4deg |
| Walker | 1.0s | `heroWalkerIn` — slides in from upper-right, ends rotated 4deg |
| Tagline | 1.3s | `heroRise` — translateY(30px) → 0, fade in, 0.6s |
| Play-now button | 1.55s | `heroSpringIn` |
| Neon waves | 0.2s | `heroFadeIn` |

Then the TV cycler starts at 1800ms (set in the inline `<script>` at the bottom of landing.html).

---

## Buttons (Play now)

All "Play now" buttons use the same `.btn-play` style — fully pill-shaped sticker buttons.

```css
.btn-play {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  height: 64px;
  padding: 0 42px;
  background: #EB10EB;             /* SMPTE magenta */
  color: #EBEBEB;                  /* SMPTE white */
  border: 3px solid #070707;       /* superblack */
  border-radius: 9999px;           /* fully pill */
  box-shadow: 6px 6px 0 0 #10EBEB; /* SMPTE cyan offset */
  font-family: "Inter", sans-serif;
  font-weight: 900;
  font-size: 22px;
  letter-spacing: 0.04em;
  text-transform: uppercase;
  text-shadow: 2px 2px 0 #8F0A8F;  /* magenta-dim */
  cursor: pointer;
  transition: transform 150ms ease, box-shadow 150ms ease;
}
.btn-play:hover  { transform: translate(3px, 3px); box-shadow: 3px 3px 0 0 #10EBEB; }
.btn-play:active { transform: translate(6px, 6px); box-shadow: 0 0 0 0 #10EBEB; }
```

Three placements on landing.html: in hero, after How It Works, after Crew. The about/privacy/terms back-link button is a separate component.

---

## Page chrome (about / privacy / terms)

All three legal pages share the same top chrome via `pages.css`:

1. **SMPTE-rail title bar** — full-width, 32px tall, centered uppercase label using two rail SVGs (`assets/ui/pageTitleLeft.svg`, `assets/ui/pageTitleRight.svg`) on either side. Label format: `<span class="bold">ABOUT </span><span class="normal">SONARCHY</span>` — first word in Inter 900, rest in Inter 700.
2. **Back arrow** — `assets/ui/back-arrow.svg` (the game's chunky illustrated arrow), 36×36px, in a 44×44px tap target, sitting **below** the title bar and left-aligned to the content column (`max-width: 760px`, `padding: 0 var(--gutter)`).
3. **Content container** — max-width 760px, centered, with `var(--gutter)` horizontal padding (clamp 20–56px).

Headings (`h2`) use Modak, clamp(28px, 5vw, 44px). Subheadings (`h3`) use Inter 900 uppercase 0.06em. Body (`p`) is Inter 500 at 16px / 1.6 line-height in `--gray-100` (#D8D8D8). Links use `--cyan` (#10EBEB) with an underline that warms on hover. Lists use `--cyan` for `::marker`.

A small "Effective Date: 12 May 2026" eyebrow tops privacy & terms; both pages end with a "Last updated" rule.

---

## Design tokens

All tokens are already declared in `app/globals.css` in the sonarchy-youtube codebase. Key ones used in this design:

### SMPTE colors

| Token | Hex | Use |
|---|---|---|
| `--smpte-superblack` | `#070707` | Page background |
| `--smpte-black` | `#101010` | Inner cards, inputs |
| `--smpte-white` | `#EBEBEB` | Primary text, borders |
| `--smpte-yellow` | `#EBEB10` | Accent highlights, frame 2 categories text |
| `--smpte-cyan` | `#10EBEB` | Drop-shadow signature, subtitles, links |
| `--smpte-green` | `#10EB10` | Success bars in dividers |
| `--smpte-magenta` | `#EB10EB` | Primary CTA color |
| `--smpte-red` | `#EB1010` | Divider bar |
| `--smpte-blue` | `#1010EB` | Divider bar |
| `--smpte-magenta-dim` | `#8F0A8F` | Button text-shadow |

### Neutrals
- `--charcoal-gray-500` (`#202020`) — surface, hero corner stripes
- `--charcoal-gray-400` (`#404040`) — dividers, borders
- `--charcoal-gray-100` (`#D8D8D8`) — muted body copy

### Typography
- **Inter** 400–900 — UI, body, titles, buttons. Loaded via Google Fonts.
- **Modak** 400 — display only (hero headings, character names, legal page H2s).
- **VT323** 400 — VCR/CRT monospace, used exclusively inside the TV screen.

### Spacing
4px base; common steps 4, 8, 12, 16, 20, 24, 32, 48. Section vertical padding: `clamp(72px, 12vw, 140px)`. Gutter: `clamp(20px, 5vw, 56px)`.

### Radii
- Buttons: `9999px` (fully pill)
- Cards / inputs: `16px`
- CRT inner screens: `8px`
- Polaroid character cards: `2px`

### Shadows
**Zero-blur hard-offset SMPTE shadows** are the brand signature:
- Magenta CTA: `6px 6px 0 0 var(--smpte-cyan)`
- Polaroid cards: `6px 6px 0 0 <smpte color>` + outer `0 18px 36px rgba(0,0,0,0.36)`
- Step projector control bar: `inset 0 -3px 0 rgba(255,255,255,0.05), inset 0 3px 0 rgba(255,255,255,0.08), 0 4px 0 rgba(0,0,0,0.6)`

### Film grain
SVG turbulence overlay applied as `position: fixed; inset: 0; mix-blend-mode: screen; opacity: 0.4` on every page. Inline data-URL — no asset needed.

---

## Assets

All assets used by the design are included in `assets/` of this bundle. Categories:

- `assets/brand/` — Sonarchy logo, hero TV frame, characters appearing in hero, 333 Games logo, "Developed with YouTube" SVG, neon line waves.
- `assets/characters/` — Casey, Walker, Vinny, Duke, Blare full-body SVGs for the Crew section.
- `assets/ui/` — `pageTitleLeft.svg`, `pageTitleRight.svg` (SMPTE-rail title decorations), `back-arrow.svg` (game's illustrated back arrow).
- `assets/textures/` — film-grain.jpg (not currently used; the design uses an inline SVG turbulence overlay instead — keep this around if you want to swap to the JPG for grain).

All SVGs come from the existing sonarchy-youtube repo (`public/images/...`) — they're shipped here so you have a complete bundle, but if your codebase already has them at known paths, prefer the canonical ones.

---

## Email and copy

- Contact email: **hello@sonarchy.com** (used on landing footer, about page, privacy & terms contact sections, GDPR rights flow).
- Play URL: **https://play.sonarchy.com**
- 333 Games studio link: **https://333games.studio**
- Studio strapline: "An independent studio making small games for the people in the room."

---

## Responsive notes

- Hero is centered with auto-scaling clamps; works from ~360px up to 1280px+.
- How It Works: 1 col → 3 col at `min-width: 768px`.
- Crew: 1 col → 2 col at 600px → 3 col at 900px.
- Footer: 1 col → 2 col at 768px; the YouTube attribution column gains a left border and 64px left padding when 2-up.
- TV text uses container queries (`cqw`), so it scales with the TV element width, not the viewport — this keeps it readable inside the bezel at any breakpoint.

---

## Files in this bundle

- `landing.html` — marketing landing page (1283 lines, fully self-contained)
- `about.html` — about page (uses `pages.css`)
- `privacy.html` — privacy policy page (uses `pages.css`)
- `terms.html` — terms of service page (uses `pages.css`)
- `pages.css` — shared styles for about/privacy/terms
- `tokens.css` — full SMPTE design token set, ready to drop into `app/globals.css` if you don't already have it
- `assets/` — all images and SVGs referenced above

The `landing.html` is intentionally self-contained — all its CSS, the SMPTE bar logic, the TV-cycler script, etc. are inline. That makes it easy to inspect every detail in one file, but you'll likely want to break it into React components when you port it. Suggested split:

- `<Hero />` (logo, TV, characters, tagline, CTA, waves) — owns the TV cycler state
- `<TVCycler frames={[…]} />` (sub-component, the only one with motion logic)
- `<HowItWorks steps={[…]} />`
- `<Crew characters={[…]} />`
- `<SiteFooter />`
- `<SmpteDivider />` (decorative bar between sections)
- Shared `<PageTitleRail label={…} />` + `<BackArrowLink href="/" />` for the legal pages

---

## What was deliberately NOT shipped

- **No favicon, no apple-touch-icon, no manifest** — set these in your Next.js `app/layout.tsx` / `metadata` per your existing pattern.
- **No analytics or consent banner** — the privacy policy mentions cookies but no cookie consent UI is in the design.
- **No i18n** — copy is English only.
- **No dark/light mode toggle** — the brand is dark by default. The light cream you see in polaroid card backgrounds is intentional contrast, not a theme flip.

---

If anything's unclear, the HTML files themselves are the source of truth — every measurement, easing, and color is in there. The README is the map; the HTML is the territory.
