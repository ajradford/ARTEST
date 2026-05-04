# ABI Presentation Generator

A Claude Code skill for creating brand-compliant HTML presentations for Acumen BI.

Implements the official Acumen BI brand guidelines (v5.1, April 2026) exactly — correct colours, fonts, slide structure, and visual hierarchy. Generates zero-dependency single-file HTML presentations that run in any browser.

## Installation

```bash
git clone https://github.com/ajradford/artest.git
cp -r artest/skills/abi-presentation ~/.claude/skills/abi-presentation
```

That's it. Claude Code auto-discovers skills in `~/.claude/skills/`.

## Usage

In any Claude Code session:

```
/abi-presentation Create a 10-slide capabilities overview for a health sector client
```

```
/abi-presentation Convert this PowerPoint to a branded HTML deck
```

```
/abi-presentation Build a 5-slide strategy roadmap for Q3 planning
```

## What it generates

- Single self-contained `.html` file — no npm, no build tools, no dependencies
- Fully keyboard-navigable (arrow keys, space, page up/down)
- Touch/swipe support for mobile and tablets
- Progress bar and navigation dots
- Optional in-browser text editing with localStorage autosave
- Optional Vercel deployment (shareable URL)
- Optional PDF export via Playwright

## Brand presets

| Preset | When to use |
|--------|-------------|
| **Acumen Dark** | Primary style — most internal and client presentations |
| **Acumen Light** | Content-heavy slides, internal reports, training materials |
| **Acumen Gradient** | Premium client pitches, executive presentations |
| **Acumen Advisory** | Strategy roadmaps, advisory findings, board-level content |

## System requirements

- Claude Code CLI
- Python + `python-pptx` (for PowerPoint conversion): `pip install python-pptx`
- Node.js + Vercel account, free tier (for URL deployment)
- Playwright (for PDF export — installed automatically on first use)

## File structure

```
SKILL.md                  Main skill — phases, brand rules, workflow
STYLE_PRESETS.md          Brand colour/font/layout specs for all presets
viewport-base.css         Mandatory responsive CSS included in every presentation
html-template.md          HTML architecture and JS feature reference
animation-patterns.md     CSS/JS animation patterns and effect guide
scripts/
  deploy.sh               Deploy to Vercel
  export-pdf.sh           Export to PDF via Playwright
  extract-pptx.py         Extract content from .pptx files
```

## Brand guidelines summary

- **Primary font:** DM Sans (web equivalent of Calibri, the official Acumen typeface)
- **Every slide:** 3px `#6A9E39` (Acumen Green) bar at top — non-negotiable
- **Dark slides:** Midnight Navy `#061626` bg / white headings / Teal `#1F798C` labels
- **Light slides:** Off White `#F7F9F8` bg (never pure white) / Green headings (large only) / Teal labels
- **Card accent bars:** rotate Teal → Brass → Steel Rose (never all green)
- **Logo:** ACUMEN in white, BI in `#6A9E39`. Dark backgrounds only.

For full brand reference see [STYLE_PRESETS.md](STYLE_PRESETS.md).

---

Brand guidelines v5.1 · Contact: Adrian Radford
