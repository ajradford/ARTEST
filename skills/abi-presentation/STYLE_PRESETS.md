# Acumen BI Style Presets

Brand-compliant visual presets for the Acumen BI Presentation Generator.
Implements brand guidelines v5.1 (April 2026). Contact: Adrian Radford.

**Viewport CSS:** For mandatory base styles, see [viewport-base.css](viewport-base.css). Include in every presentation.

---

## Brand Colour Reference

```
PRIMARY
  Acumen Green   #6A9E39   Logo colour. 3px top bar, headings (large only), CTAs.
  Charcoal       #404040   Body text, dark slide panels.
  Midnight Navy  #061626   Dark slide backgrounds, covers.

SECONDARY
  Teal           #1F798C   Section labels, subheadings, links, active states.
  Brass          #B5892A   Callouts, key metrics, advisory accent, card bar 2.
  Steel Rose     #8C5470   Card bar 3, dark-slide highlights, data viz series 4.

STATUS — system states only, never decorative
  Green #6A9E39 / Amber #F5A623 / Coral #E05947 / Grey #9FA09E

NEUTRALS
  Off White  #F7F9F8   Preferred light slide background. Never use pure #FFFFFF.
  Cool Grey  #E8ECEB   Card fills, alt table rows.
  Mid Grey   #D1D8D5   Borders, dividers, connector lines.
  White      #FFFFFF   Card backgrounds and reverse text on dark slides.

TONAL SCALES (500 = core value)
  Green:  50:#F0F8E8  200:#B8DFA0  500:#6A9E39  600:#5A8B2E  700:#4E7A28  900:#3A5C1D
  Teal:   50:#F5F6F7  200:#CADEE1  500:#1F798C  600:#186675  700:#12515E  900:#0A3037
  Brass:  50:#F7F6F5  200:#E1DACA  500:#B5892A  600:#967121  700:#785A19  900:#47350E
  Rose:   50:#F6F5F6  200:#DAD1D6  500:#8C5470  600:#73435B  700:#5C3448  900:#361E2A
  Grey:   50:#F7F9F8  100:#E8ECEB  200:#D1D8D5  400:#9FA09E  800:#404040  950:#061626

GRADIENTS (all 135°, never behind body text)
  Navy → Teal:         #061626 → #1F798C   Hero sections, covers
  Teal → Green:        #1F798C → #6A9E39   Section dividers
  Navy → Teal → Rose:  #061626 → #1F798C → #8C5470   Premium, multi-service
  Navy → Brass:        #061626 → #B5892A   Advisory and strategy
```

---

## Brand Fonts

```
DM Sans     Web-safe equivalent of Calibri (official Acumen presentation typeface)
DM Mono     Numeric and data callouts

Google Fonts link for every Acumen presentation:
https://fonts.googleapis.com/css2?family=DM+Sans:ital,wght@0,300;0,400;0,500;0,600;1,300&family=DM+Mono:wght@400&display=swap

NEVER USE: Inter, Roboto, Arial, system fonts as display typeface
```

---

## Acumen BI Presets

### Preset A1 — Acumen Dark ★ Default

**Vibe:** Professional, credible, premium data analytics. The primary Acumen presentation style.

**Use for:** Most internal and client presentations, capabilities overviews, project findings.

**Layout:** Midnight Navy background. 3px Green top bar. Thin vertical left accent line. Content left-aligned or centered. Subtle Teal radial atmosphere orb. Section labels in Teal, headings in white.

**Typography:**
- Display: `DM Sans` (600)
- Body: `DM Sans` (300/400)
- Numbers/data: `DM Mono` (400)

**Colors:**
```css
:root {
    --bg-primary:    #061626;               /* Midnight Navy */
    --accent-green:  #6A9E39;               /* Top bar (non-negotiable) */
    --accent-teal:   #1F798C;               /* Labels, subheadings */
    --accent-brass:  #B5892A;               /* Callouts, metrics, card bar 2 */
    --accent-rose:   #8C5470;               /* Card bar 3 */
    --text-heading:  #ffffff;
    --text-sub:      rgba(255,255,255,0.55);
    --text-body:     rgba(255,255,255,0.40);
    --text-caption:  rgba(255,255,255,0.28);
    --text-label:    #1F798C;               /* Teal for section labels */
    --card-bg:       rgba(255,255,255,0.05);
    --card-border:   rgba(255,255,255,0.07);
    --atmosphere:    rgba(31,121,140,0.10); /* Teal orb */
    --v-line:        rgba(106,158,57,0.35); /* Left accent line */
}
```

**Signature Elements:**
- `3px` `#6A9E39` bar: `position: absolute; top: 0; left: 0; right: 0; height: 3px; background: #6A9E39; z-index: 10`
- Teal atmosphere: `radial-gradient(ellipse at 75% 55%, rgba(31,121,140,0.12), transparent 55%)` — positioned as a pseudo-element or absolute div
- Left accent line: `1px solid` gradient `transparent → rgba(106,158,57,0.4) → transparent`, runs full height, `left: clamp(2rem,5vw,5rem)`
- Section labels: `DM Sans` 500, `#1F798C`, `text-transform: uppercase`, `letter-spacing: 0.18em`, `font-size: clamp(0.58rem,0.85vw,0.72rem)`
- Headings: `DM Sans` 600, `#ffffff`, `font-size: clamp(1.6rem,4vw,3.2rem)`, `line-height: 1.1`
- Cards: `background: rgba(255,255,255,0.05)`, `border: 1px solid rgba(255,255,255,0.07)`, `border-radius: 4px`, `2px` top accent bar: card 1=Teal, card 2=Brass, card 3=Rose
- Slide counter: bottom-right, `DM Mono` 400, `rgba(255,255,255,0.18)`, `font-size: clamp(0.6rem,0.9vw,0.75rem)`

---

### Preset A2 — Acumen Light

**Vibe:** Clean, approachable, content-heavy. Secondary Acumen style.

**Use for:** Internal reports, detailed findings, process documentation, training materials.

**Layout:** Off White background. 3px Green top bar. Thin Teal vertical accent line left. Green only on large headings. Teal for labels. White content cards with subtle border and shadow.

**Typography:**
- Display: `DM Sans` (600)
- Body: `DM Sans` (300/400)
- Numbers/data: `DM Mono` (400)

**Colors:**
```css
:root {
    --bg-primary:    #F7F9F8;               /* Off White — NEVER use #FFFFFF */
    --bg-card:       #FFFFFF;
    --bg-alt:        #E8ECEB;               /* Alt row fills */
    --accent-green:  #6A9E39;               /* Top bar + large headings only */
    --accent-teal:   #1F798C;               /* Labels, subheadings */
    --accent-brass:  #B5892A;               /* Callouts, key metrics */
    --accent-rose:   #8C5470;               /* Card bar 3 */
    --text-heading:  #6A9E39;               /* Large headings only */
    --text-heading-sm: #2F3A40;             /* Smaller headings */
    --text-body:     #2F3A40;
    --text-mid:      #6B7280;
    --text-caption:  #9CA3AF;
    --text-label:    #1F798C;
    --border:        rgba(0,0,0,0.08);
    --card-shadow:   0 1px 3px rgba(0,0,0,0.06);
    --v-line:        rgba(31,121,140,0.45); /* Teal left accent line */
}
```

**Signature Elements:**
- `3px` `#6A9E39` bar at very top (same as all Acumen slides)
- Left accent line: `1px` gradient, Teal-tinted
- Green heading rule: **only apply `color: #6A9E39` to headings set at `font-size > 24px`**. Smaller headings use `#2F3A40`.
- White cards: `background: #FFFFFF`, `border: 1px solid rgba(0,0,0,0.08)`, `border-radius: 4px`, `box-shadow: 0 1px 3px rgba(0,0,0,0.06)`, `2px` top accent bar rotating Teal → Brass → Rose
- Table rows: alternate `#F7F9F8` / `#FFFFFF`, header row `#404040` bg with `rgba(255,255,255,0.6)` text
- Dividers: `1px solid #D1D8D5`

---

### Preset A3 — Acumen Gradient

**Vibe:** Premium, strategic, high-stakes. The most visually impactful Acumen style.

**Use for:** Client pitches, executive presentations, capability showcases, proposal covers.

**Layout:** Full-bleed Navy→Teal gradient. White text throughout. Green top bar. Subtle geometric circle outlines at low opacity. Content centred or split-panel.

**Typography:**
- Display: `DM Sans` (600)
- Body: `DM Sans` (300/400)
- Numbers/data: `DM Mono` (400)

**Colors:**
```css
:root {
    --bg-gradient:   linear-gradient(135deg, #061626 0%, #1F798C 100%);
    --accent-green:  #6A9E39;               /* Top bar */
    --accent-brass:  #B5892A;               /* Stats, callouts on gradient */
    --text-heading:  #ffffff;
    --text-sub:      rgba(255,255,255,0.65);
    --text-body:     rgba(255,255,255,0.50);
    --text-label:    rgba(255,255,255,0.60);
    --card-bg:       rgba(255,255,255,0.08);
    --card-border:   rgba(255,255,255,0.14);
}
```

**Signature Elements:**
- Background: `background: linear-gradient(135deg, #061626 0%, #1F798C 100%)`
- `3px` `#6A9E39` top bar
- Geometric decorative circles: `border-radius: 50%`, `border: 1px solid rgba(255,255,255,0.07)` — 2–3 overlapping at varying sizes, `pointer-events: none`
- Glass cards: `background: rgba(255,255,255,0.08)`, `border: 1px solid rgba(255,255,255,0.14)`, `border-radius: 4px`
- Key stats use Brass `#B5892A` — warm contrast against the cool gradient
- All text: white or white with opacity. No coloured text on gradient.

---

### Preset A4 — Acumen Advisory

**Vibe:** Advisory, strategic authority, financial services. Warm and credible.

**Use for:** Strategy roadmaps, advisory findings, investment cases, board-level content.

**Layout:** Midnight Navy background. Brass replaces Teal as the primary accent. Green top bar always. Warm Brass orb atmosphere. Cards with Brass accent bars.

**Typography:**
- Display: `DM Sans` (600)
- Body: `DM Sans` (300/400)
- Numbers/data: `DM Mono` (400)

**Colors:**
```css
:root {
    --bg-primary:    #061626;               /* Midnight Navy */
    --accent-green:  #6A9E39;               /* Top bar only — always green */
    --accent-brass:  #B5892A;               /* Primary accent (replaces Teal) */
    --accent-teal:   #1F798C;               /* Secondary accent */
    --accent-rose:   #8C5470;               /* Tertiary accent */
    --text-heading:  #ffffff;
    --text-sub:      rgba(255,255,255,0.55);
    --text-body:     rgba(255,255,255,0.40);
    --text-label:    #B5892A;               /* Brass labels (not teal) */
    --card-bg:       rgba(181,137,42,0.07);
    --card-border:   rgba(181,137,42,0.18);
    --atmosphere:    rgba(181,137,42,0.08); /* Brass orb */
    --v-line:        rgba(181,137,42,0.32);
}
```

**Signature Elements:**
- `3px` `#6A9E39` top bar — **never Brass, always Green**
- Brass atmosphere orb: `radial-gradient(ellipse at 80% 25%, rgba(181,137,42,0.12), transparent 55%)`
- Left accent line: Brass-tinted gradient
- Section labels: `DM Sans` 500, `#B5892A` (Brass instead of Teal)
- Cards: warm dark fill with `2px solid #B5892A` top border
- Key metric callouts: `DM Mono`, `#B5892A`, large — e.g. `font-size: clamp(1.8rem,4vw,3.5rem)`

---

## General Library

Available for non-Acumen presentations or where the user explicitly requests a different aesthetic.

### 1. Bold Signal
**Typography:** `Archivo Black` (900) + `Space Grotesk` (400/500)
**Colors:** Dark `#1a1a1a`, card `#FF5722`, text white
**Signature:** Colored card panel. Large section numbers.

### 2. Electric Studio
**Typography:** `Manrope` (800/400/500)
**Colors:** Black `#0a0a0a`, white, blue `#4361ee`
**Signature:** Two-panel vertical split. Accent bar on edge.

### 3. Creative Voltage
**Typography:** `Syne` (700/800) + `Space Mono` (400/700)
**Colors:** Electric blue `#0066ff`, dark `#1a1a2e`, neon `#d4ff00`
**Signature:** Split panels, halftone textures, neon badges.

### 4. Dark Botanical
**Typography:** `Cormorant` (400/600 italic) + `IBM Plex Sans` (300/400)
**Colors:** Near-black `#0f0f0f`, cream `#e8e4df`, gold `#d4a574`
**Signature:** Blurred gradient blobs. Thin accent lines. Italic serif.

### 5. Notebook Tabs
**Typography:** `Bodoni Moda` (400/700) + `DM Sans` (400/500)
**Colors:** Dark outer `#2d2d2d`, cream page `#f8f6f1`
**Signature:** Paper card on dark bg. Coloured tabs. Binder holes.

### 6. Swiss Modern
**Typography:** `Archivo` (800) + `Nunito` (400)
**Colors:** White, black, red `#ff3300`
**Signature:** Visible grid, asymmetric layouts, geometric shapes.

### 7. Neon Cyber
**Typography:** `Clash Display` + `Satoshi` (Fontshare)
**Colors:** Navy `#0a0f1c`, cyan `#00ffcc`, magenta `#ff00aa`
**Signature:** Particle backgrounds, neon glow, grid patterns.

---

## CSS Gotchas

**Negating CSS functions — WRONG (silently ignored):**
```css
right: -clamp(28px, 3.5vw, 44px);   /* Browser ignores this */
```
**CORRECT:**
```css
right: calc(-1 * clamp(28px, 3.5vw, 44px));  /* Works */
```
