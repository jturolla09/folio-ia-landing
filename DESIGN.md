# Design System — Folio AI Landing

Generated from `index.html` via `/impeccable extract`. Use this alongside `PRODUCT.md` in any repo that shares this visual identity.

---

## Color Strategy

**Drenched cobalt.** The page surface IS the color. Deep navy-cobalt carries the entire brand weight; warm cream paper sections provide deliberate, rhythmic relief. Never gradient text. No glassmorphism.

---

## Tokens

```css
:root {
  /* Cobalt surface scale */
  --cobalt:        oklch(0.14 0.04 264);   /* base page surface */
  --cobalt-mid:    oklch(0.18 0.05 264);   /* elevated cobalt layer */
  --cobalt-deep:   oklch(0.10 0.03 264);   /* nav-scrolled, deepest layer */
  --cobalt-accent: oklch(0.50 0.20 264);   /* interactive blue, focus rings */

  /* Paper/light surfaces */
  --cream:         oklch(0.93 0.025 78);   /* warm highlight, CTA buttons */
  --paper:         oklch(0.97 0.008 78);   /* paper section background, mockup surfaces */
  --paper-border:  oklch(0.90 0.012 264);  /* borders on light surfaces */

  /* Text on paper */
  --ink:           oklch(0.18 0.018 264);  /* primary text */
  --ink-soft:      oklch(0.44 0.04 264);   /* secondary text — WCAG AA minimum */

  /* Text on cobalt */
  --on-cobalt:     oklch(0.96 0.006 264);  /* primary text */
  --on-cobalt-dim: oklch(0.62 0.04 264);   /* secondary text, eyebrows, sub-labels */

  /* Status colors */
  --ok:            oklch(0.62 0.14 148);   /* green value/badge */
  --ok-bg:         oklch(0.96 0.04 148);
  --warn:          oklch(0.68 0.13 56);    /* amber value/badge */
  --warn-bg:       oklch(0.97 0.04 56);
  --low:           oklch(0.58 0.10 240);   /* low-normal blue */
  --low-bg:        oklch(0.96 0.03 240);
  --error-border:  oklch(0.65 0.15 24);    /* form validation red */

  /* System */
  --font: 'General Sans', system-ui, -apple-system, sans-serif;
  --ease-out-quart: cubic-bezier(0.25, 1, 0.5, 1);
}
```

**Rules:**
- Never use `#000` / `#fff` — tint every neutral toward the brand hue (chroma ≥ 0.004)
- `--ink-soft` is the WCAG AA floor — nothing secondary goes lighter on paper
- On cobalt backgrounds always use `--on-cobalt` / `--on-cobalt-dim`, never `--ink`
- Status badges use the `*-bg` token as background and the base token as text/icon color

---

## Surfaces

### `.cobalt-surface`
Deep cobalt with a two-point radial gradient atmosphere (warm glow upper-left, dark shadow upper-right). Applied to: hero, Beat 2 (metrics), Beat 3 (doctor copy), footer CTA.

```css
.cobalt-surface {
  background-color: var(--cobalt);
  background-image:
    radial-gradient(ellipse 60% 50% at 5% 30%,  oklch(0.22 0.08 264 / 0.6) 0%, transparent 100%),
    radial-gradient(ellipse 40% 40% at 90% 10%,  oklch(0.10 0.04 256 / 0.8) 0%, transparent 100%);
}
```

### `.paper-surface`
Warm cream relief. Applied to: Beat 1 (extraction), Beat 3 (trust/doctor quote).

```css
.paper-surface { background-color: var(--paper); }
```

### Section rhythm
`cobalt (hero) → paper (Beat 1) → cobalt (Beat 2) → paper (Beat 3) → cobalt (footer)`

Dividers between sections use `.beat-rule`:
```css
.beat-rule {
  border: none;
  border-top: 1px solid oklch(0.44 0.12 264 / 0.45);
  margin: 0;
}
```

---

## Typography

Font: **General Sans** (400 / 500 / 600 / 700) via Fontshare.

```
<link rel="stylesheet" href="https://api.fontshare.com/v2/css?f[]=general-sans@400,500,600,700&display=swap">
```

| Role | Size | Weight | Tracking | Max-width | Color |
|---|---|---|---|---|---|
| Hero headline | `clamp(2.4rem, 4.5vw, 4.2rem)` | 700 | -0.035em | 14ch | `--on-cobalt` |
| Beat headline | `clamp(2rem, 3.8vw, 3.6rem)` | 700 | -0.03em | 20ch | context-aware* |
| Caption h2 | `clamp(1.6rem, 2.8vw, 2.6rem)` | 700 | -0.03em | — | context-aware* |
| Hero sub / Beat body | `clamp(1rem, 1.5vw, 1.125rem)` | 400 | — | 52ch | context-aware* |
| Eyebrow / Beat number | `0.6875rem` | 700 | 0.14em | — | dim |
| Body copy | `1rem` | 400 | — | — | context-aware* |

*Context-aware: `--ink` / `--ink-soft` on paper; `--on-cobalt` / `--on-cobalt-dim` on cobalt. Achieved via `.cobalt-surface .beat-* { color: var(--on-cobalt*); }` overrides — base styles default to ink tokens.

**Rules:** body line length ≤ 52ch; scale steps ≥ 1.25× ratio; no flat hierarchies.

---

## Layout

```css
.grid {
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  column-gap: clamp(16px, 2vw, 24px);
  max-width: 1280px;
  margin-inline: auto;
  padding-inline: clamp(24px, 6vw, 80px);
}
```

| Zone | Columns |
|---|---|
| Hero copy | 1 / 8 |
| Hero phone | 8 / 13 |
| Beat inner (full) | 1 / -1 |
| Beat split (2-col) | `grid-template-columns: 1fr 1fr`, `gap: clamp(40px, 5vw, 80px)` |

**Section padding:** `clamp(80px, 10vh, 130px)` block.

**Breakpoints:**
- `≤ 960px` — hero/beats collapse to 1 column; footer CTA stacks
- `≤ 680px` — phone mockup hidden; form stacks; footer meta wraps

---

## Shadow System

Shadows use cobalt-tinted values throughout. Opacity scales with surface contrast.

### On cobalt surfaces (app-frame, phone shell)
```css
/* App frame floating on cobalt */
box-shadow:
  0 0 0 1px oklch(0.30 0.06 264 / 0.40),
  0 28px 72px oklch(0.06 0.03 264 / 0.60),
  0 6px 20px  oklch(0.06 0.03 264 / 0.32);

/* Phone shell */
box-shadow:
  0 0 0 1px oklch(0.28 0.06 264 / 0.6),
  0 40px 90px oklch(0.06 0.04 264 / 0.9),
  0 8px 24px  oklch(0.06 0.04 264 / 0.5);
```

### On paper surfaces (extraction panel, cards)
```css
/* Elevated card on paper */
box-shadow:
  0 2px 8px   oklch(0.40 0.04 264 / 0.08),
  0 16px 48px oklch(0.30 0.04 264 / 0.13),
  0 4px 16px  oklch(0.30 0.04 264 / 0.07);
```

---

## Motion

All motion uses `--ease-out-quart`. No bounce. No elastic. No layout-property animation.

```css
--ease-out-quart: cubic-bezier(0.25, 1, 0.5, 1);
```

### Scroll reveal
Elements with `data-reveal` start invisible (`opacity: 0; transform: translateY(18px)`), animate in when entering viewport via IntersectionObserver. Stagger delays via `data-delay="1"` / `"2"` / `"3"` (0.08s increments).

```html
<h2 data-reveal>Headline</h2>
<p  data-reveal data-delay="1">Body text</p>
```

`prefers-reduced-motion: reduce` disables all reveals and smooth scroll.

### Nav scroll state
`.nav--scrolled` applied via IntersectionObserver on the hero section. Transition: 0.3s `background` + `border-bottom-color` with `--ease-out-quart`.

---

## Components

### Waitlist form
```html
<form class="waitlist-form" data-which="hero|cta" novalidate>
  <div class="form-row">
    <label for="id" class="sr-only">Seu e-mail</label>
    <input type="email" id="id" class="form-email" placeholder="seu@email.com">
    <button type="submit" class="form-submit">Entrar na lista</button>
  </div>
  <p class="form-feedback" role="alert" hidden></p>
  <div class="cf-turnstile" data-sitekey="..." data-callback="onTurnstile{Which}" ...
       id="turnstile-{which}"></div>
  <p class="form-trust">...</p>
</form>
```

Cloudflare Turnstile widget hidden by default (`display: none`). Revealed only if the token isn't ready when user clicks submit. Auto-submits once token resolves. 10s hard fallback re-enables button.

States: `:focus` (accent border), `[disabled]` (opacity 0.55, `cursor: wait`), success (`.form-success` replaces form).

### Navigation
Fixed, z-index 100. Transparent at top; `.nav--scrolled` adds `cobalt-deep` background when hero section leaves viewport.

### Beat layout

**Single column (Beat 3):**
```html
<section class="section paper-surface|cobalt-surface">
  <div class="grid">
    <div class="beat-inner">
      <span class="beat-num" data-reveal>02</span>
      <h2 class="beat-headline" data-reveal data-delay="1">...</h2>
      <p class="beat-body" data-reveal data-delay="2">...</p>
    </div>
  </div>
</section>
```

**Split (Beat 1 — text + demo panel):**
```html
<div class="beat-split">
  <div class="beat-inner">...</div>
  <div class="extraction-panel" ...>...</div>
</div>
```

### Phone mockup
```html
<div class="phone-shell">
  <div class="phone-island"></div>   <!-- Dynamic Island, absolute positioned -->
  <div class="phone-screen">
    <!-- app content, padding-top: 54px clears island -->
  </div>
</div>
```

Shell: 270px wide, 48px border-radius, `overflow: hidden` (clips screen to shell radius — no inner bezels). Island: `position: absolute; top: 14px; left: 50%; transform: translateX(-50%)`. Hidden at ≤ 680px.

### Extraction panel
White demo card (`oklch(0.99 0.004 264)`) with `--paper-border` border and soft elevated shadow. Used on paper surfaces.

### App frame
White demo UI frame (`oklch(0.99 0.004 264)`) with strong cobalt lifting shadow. Used inside `.cobalt-surface` sections.

---

## Accessibility

- **WCAG AA contrast**: `--ink-soft` (`oklch(0.44 0.04 264)`) is the minimum for secondary text on paper. Do not go lighter.
- **Screen reader**: `.sr-only` for labels; `role="alert"` on form feedback; `aria-labelledby` on all sections; `aria-hidden="true"` on decorative elements.
- **Keyboard**: form submit via Enter; all interactive elements focusable; focus rings use `--cobalt-accent` / `--cream` outlines.
- **Reduced motion**: `@media (prefers-reduced-motion: reduce)` disables all `[data-reveal]` transitions.
