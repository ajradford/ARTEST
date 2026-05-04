---
name: abi-presentation
description: Create brand-compliant HTML presentations for Acumen BI. Implements the official Acumen BI brand guidelines (v5.1) exactly — correct colours, fonts, slide structure, and visual hierarchy. Use when an Acumen BI team member needs a presentation, pitch deck, client deliverable, or internal slide deck. Also handles PPT/PPTX conversion. Invoke with /abi-presentation.
---

# Acumen BI Presentation Generator

Create zero-dependency, animation-rich HTML presentations that run entirely in the browser — built to Acumen BI brand guidelines.

## About Acumen BI

Acumen BI is a New Zealand owned and operated data and analytics consultancy with offices in Auckland and Wellington. We cover the full data spectrum: advisory and strategy, operating models, data engineering, analytics, visualisation, and architecture. Deep experience in Health and Government; strong coverage in Insurance, Financial Services, Media, and Manufacturing.

**Tagline (primary):** Advanced Analytics · AI-Powered Intelligence
**Never use:** "Fast, Simple, Effective Business Intelligence"

**Tone:** Straightforward, credible, genuine kiwi directness. Outcome-focused. Use "we work alongside your team". Reference AI specifically and practically. No jargon, no passive voice.

---

## Core Principles

1. **Zero Dependencies** — Single HTML files with inline CSS/JS. No npm, no build tools.
2. **Brand First** — Acumen BI colour, font, and layout rules are non-negotiable. Apply them exactly.
3. **Show, Don't Tell** — Generate visual previews, not abstract choices.
4. **Viewport Fitting (NON-NEGOTIABLE)** — Every slide MUST fit exactly within 100vh. No scrolling within slides, ever. Content overflows? Split into multiple slides.

---

## Non-Negotiable Brand Rules

These apply to **every** Acumen BI slide, no exceptions:

- Every `.slide` has a **`3px solid #6A9E39` bar** spanning the full width at the very top (`position: absolute; top: 0; left: 0; right: 0; height: 3px; background: #6A9E39; z-index: 10`)
- **Never use pure white `#FFFFFF` as a slide background** — use Off White `#F7F9F8` for light slides
- **Card accent bars** rotate through Teal `#1F798C` → Brass `#B5892A` → Steel Rose `#8C5470`. Never all green.
- **Logo rule:** ACUMEN in white, BI in `#6A9E39`. Dark backgrounds only — never on a green background.
- **Font:** `DM Sans` (Google Fonts) is the brand web font — the closest available equivalent to Calibri, the official Acumen presentation typeface. Always use DM Sans. Never use Inter, Roboto, Arial, or system fonts as display.
- **Acumen Green `#6A9E39` achieves 3.0:1 contrast on Off White** — qualifying for large text (headings) only. Reserve green for primary headings and the 3px top bar. Use Teal `#1F798C` for section labels and subheadings.

---

## Viewport Fitting Rules

These invariants apply to EVERY slide:

- Every `.slide` must have `height: 100vh; height: 100dvh; overflow: hidden;`
- ALL font sizes and spacing must use `clamp(min, preferred, max)` — never fixed px/rem
- Content containers need `max-height` constraints
- Images: `max-height: min(50vh, 400px)`
- Breakpoints required for heights: 700px, 600px, 500px
- Include `prefers-reduced-motion` support
- Never negate CSS functions directly (`-clamp()`, `-min()`, `-max()` are silently ignored) — use `calc(-1 * clamp(...))` instead

**When generating, read `viewport-base.css` and include its full contents in every presentation.**

### Content Density Limits Per Slide

| Slide Type    | Maximum Content                                            |
| ------------- | ---------------------------------------------------------- |
| Title slide   | 1 heading + 1 subtitle + optional tagline                  |
| Content slide | 1 heading + 4–6 bullet points OR 1 heading + 2 paragraphs |
| Feature grid  | 1 heading + 6 cards maximum (2×3 or 3×2)                  |
| Code slide    | 1 heading + 8–10 lines of code                            |
| Quote slide   | 1 quote (max 3 lines) + attribution                        |
| Image slide   | 1 heading + 1 image (max 60vh height)                      |

**Content exceeds limits? Split into multiple slides. Never cram, never scroll.**

---

## Phase 0: Detect Mode

Determine what the user wants:

- **Mode A: New Presentation** — Create from scratch. Go to Phase 1.
- **Mode B: PPT Conversion** — Convert a .pptx file. Go to Phase 4.
- **Mode C: Enhancement** — Improve an existing HTML presentation. Read it, understand it, enhance. **Follow Mode C modification rules below.**

### Mode C: Modification Rules

When enhancing existing presentations, viewport fitting is the biggest risk:

1. **Before adding content:** Count existing elements, check against density limits
2. **Adding images:** Must have `max-height: min(50vh, 400px)`. If slide already has max content, split into two slides
3. **Adding text:** Max 4–6 bullets per slide. Exceeds limits? Split into continuation slides
4. **After ANY modification, verify:** `.slide` has `overflow: hidden`, new elements use `clamp()`, images have viewport-relative max-height, content fits at 1280×720
5. **Proactively reorganise:** If modifications will cause overflow, automatically split content and inform the user

---

## Phase 1: Content Discovery

**Ask ALL questions in a single AskUserQuestion call.**

**Question 1 — Purpose** (header: "Purpose"):
What is this presentation for?
- Client pitch / Capabilities overview
- Internal presentation / Team update
- Project delivery / Data findings
- Conference talk / External event

**Question 2 — Length** (header: "Length"):
Approximately how many slides?
- Short 5–10 / Medium 10–20 / Long 20+

**Question 3 — Content** (header: "Content"):
Do you have content ready?
- All content ready / Rough notes / Topic only

**Question 4 — Editing** (header: "Editing"):
Do you need to edit text directly in the browser after generation?
- "Yes (Recommended)" — edit in-browser, auto-save to localStorage, export file
- "No" — presentation only

If user has content, ask them to share it.

---

## Phase 2: Style Selection

**Skip the mood/vibe questions.** Acumen BI presentations always use a brand preset. Ask only:

**Question: Which style suits this presentation?** (header: "Style")

- **Acumen Dark** (Recommended for most) — Midnight Navy bg, the primary brand style
- **Acumen Light** — Off White bg, clean, ideal for content-heavy or internal slides
- **Acumen Gradient** — Navy→Teal gradient, premium client-facing pitches
- **Acumen Advisory** — Navy bg with Brass accents, strategy and advisory content

Read [STYLE_PRESETS.md](STYLE_PRESETS.md) for the full specification of each preset before generating.

---

## Phase 3: Generate Presentation

Generate the full presentation using content from Phase 1 and the chosen style from Phase 2.

**Before generating, read these supporting files:**

- [html-template.md](html-template.md) — HTML architecture and JS features
- [viewport-base.css](viewport-base.css) — Mandatory CSS (include in full)
- [animation-patterns.md](animation-patterns.md) — Animation reference
- [STYLE_PRESETS.md](STYLE_PRESETS.md) — Brand colour and layout spec

**Key requirements:**

- Single self-contained HTML file, all CSS/JS inline
- Include the FULL contents of viewport-base.css in the `<style>` block
- Font: `DM Sans` from Google Fonts — `https://fonts.googleapis.com/css2?family=DM+Sans:ital,wght@0,300;0,400;0,500;0,600;1,300&family=DM+Mono:wght@400&display=swap`
- Every slide must have the 3px Green top bar
- Every slide must have `height: 100vh; height: 100dvh; overflow: hidden`
- Add detailed comments explaining each section with `/* === SECTION NAME === */` headers

### Slide Structure Template

Every content slide follows this layout hierarchy:

```
[3px Green bar — position: absolute, top 0]
[Optional: vertical accent line, 1px, left edge]

Section label    → DM Sans 500, Teal #1F798C, uppercase, letter-spacing: 0.18em
Heading          → DM Sans 600, clamp(1.4rem, 3.5vw, 2.8rem)
                   Dark slides: #ffffff
                   Light slides: #6A9E39 (large only) or #2F3A40 (smaller)
Subheading       → DM Sans 400, Teal #1F798C
Body text        → DM Sans 300, line-height: 1.7
                   Dark: rgba(255,255,255,0.55)
                   Light: #2F3A40
Captions         → Dark: rgba(255,255,255,0.38) | Light: #6B7280

Content cards    → 4px border-radius, 2px top accent bar (Teal/Brass/Rose rotating)
                   Dark: rgba(255,255,255,0.05) bg, rgba(255,255,255,0.07) border
                   Light: #FFFFFF bg, rgba(0,0,0,0.08) border

Slide counter    → bottom-right, DM Mono, very low opacity
```

---

## Phase 4: PPT Conversion

When converting PowerPoint files:

1. **Extract content** — Run `python scripts/extract-pptx.py <input.pptx> <output_dir>` (install python-pptx if needed: `pip install python-pptx`)
2. **Confirm with user** — Present extracted slide titles, content summaries, and image counts
3. **Style selection** — Ask which Acumen brand style (Phase 2)
4. **Generate HTML** — Convert to chosen style, preserving all text, images (from assets/), slide order, and speaker notes (as HTML comments)

---

## Phase 5: Delivery

1. **Clean up** — Delete `.claude-design/slide-previews/` if it exists
2. **Open** — Use `open [filename].html` to launch in browser
3. **Summarise** — Tell the user:
   - File location, style name, slide count
   - Navigation: Arrow keys, Space, scroll/swipe, click nav dots
   - How to customise: `:root` CSS variables for colours, font link for typography
   - If inline editing was enabled: Hover top-left corner or press E to enter edit mode, click any text to edit, Ctrl+S to save

---

## Phase 6: Share & Export (Optional)

After delivery, ask: *"Would you like to share this presentation? I can deploy it to a live URL or export it as a PDF."*

Options: Deploy to URL / Export to PDF / Both / No thanks

### 6A: Deploy to a Live URL (Vercel)

```bash
bash scripts/deploy.sh <path-to-presentation>
```

Guide the user through Vercel signup if needed. The script handles folder or single-file deployments.

**Deploy gotchas:**
- Local images must travel with the HTML — the script auto-detects `src="..."` references
- Redeploying overwrites the same URL

### 6B: Export to PDF

```bash
bash scripts/export-pdf.sh <path-to-html> [output.pdf]
```

Renders at 1920×1080. Use `--compact` flag if PDF exceeds 10MB (renders at 1280×720 instead).

---

## Supporting Files

| File                     | Purpose                                          | When to Read             |
| ------------------------ | ------------------------------------------------ | ------------------------ |
| [STYLE_PRESETS.md](STYLE_PRESETS.md)   | Acumen BI brand presets + general library | Phase 2 & 3 |
| [viewport-base.css](viewport-base.css) | Mandatory responsive CSS                  | Phase 3     |
| [html-template.md](html-template.md)   | HTML structure, JS features               | Phase 3     |
| [animation-patterns.md](animation-patterns.md) | CSS/JS animation snippets         | Phase 3     |
| [scripts/extract-pptx.py](scripts/extract-pptx.py) | PPT content extraction         | Phase 4     |
| [scripts/deploy.sh](scripts/deploy.sh) | Deploy to Vercel                          | Phase 6     |
| [scripts/export-pdf.sh](scripts/export-pdf.sh) | Export to PDF                       | Phase 6     |
