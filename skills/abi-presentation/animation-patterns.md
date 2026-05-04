# Animation Patterns Reference

Use this reference when generating presentations. Match animations to the intended feeling.

## Effect-to-Feeling Guide

| Feeling | Animations | Visual Cues |
|---------|-----------|-------------|
| **Dramatic / Cinematic** | Slow fade-ins (1-1.5s), large scale transitions (0.9 to 1), parallax scrolling | Dark backgrounds, spotlight effects, full-bleed images |
| **Techy / Futuristic** | Neon glow (box-shadow), glitch/scramble text, grid reveals | Particle systems (canvas), grid patterns, monospace accents, cyan/magenta/electric blue |
| **Playful / Friendly** | Bouncy easing (spring physics), floating/bobbing | Rounded corners, pastel/bright colors, hand-drawn elements |
| **Professional / Corporate** | Subtle fast animations (200-300ms), clean slides | Navy/slate/charcoal, precise spacing, data visualization focus |
| **Calm / Minimal** | Very slow subtle motion, gentle fades | High whitespace, muted palette, serif typography, generous padding |
| **Editorial / Magazine** | Staggered text reveals, image-text interplay | Strong type hierarchy, pull quotes, grid-breaking layouts, serif headlines + sans body |

## Acumen BI Animation Style

For all Acumen brand presets, use **Professional / Corporate** animation patterns:

- Fade + slide up: `opacity 0→1`, `translateY(20px)→0`, duration `0.65s`, easing `cubic-bezier(0.16, 1, 0.3, 1)`
- Stagger delay: `0.08s` per element (`delay-1` through `delay-6`)
- Avoid: bouncy easing, neon glow, particle effects, parallax — these clash with the brand's credibility
- Atmosphere orbs (Dark/Advisory presets): `animation: drift 9-13s ease-in-out infinite alternate` at very low opacity

## Entrance Animations

```css
/* Fade + Slide Up (primary — use for all Acumen slides) */
.reveal {
    opacity: 0;
    transform: translateY(22px);
    transition: opacity 0.65s var(--ease-out-expo),
                transform 0.65s var(--ease-out-expo);
}
.slide.visible .reveal {
    opacity: 1;
    transform: translateY(0);
}

/* Scale In */
.reveal-scale {
    opacity: 0;
    transform: scale(0.92);
    transition: opacity 0.65s, transform 0.65s var(--ease-out-expo);
}

/* Slide from Left */
.reveal-left {
    opacity: 0;
    transform: translateX(-28px);
    transition: opacity 0.7s, transform 0.7s var(--ease-out-expo);
}

/* Blur In */
.reveal-blur {
    opacity: 0;
    filter: blur(8px);
    transition: opacity 0.9s, filter 0.9s var(--ease-out-expo);
}
```

## Background Effects

```css
/* Acumen atmosphere orb (Dark/Advisory presets) */
.atmosphere {
    position: absolute;
    border-radius: 50%;
    filter: blur(90px);
    pointer-events: none;
    animation: drift 9s ease-in-out infinite alternate;
}
@keyframes drift {
    from { transform: translate(0, 0) scale(1); }
    to   { transform: translate(3%, 4%) scale(1.06); }
}

/* Grid Pattern — subtle structural lines */
.grid-bg {
    background-image:
        linear-gradient(rgba(255,255,255,0.03) 1px, transparent 1px),
        linear-gradient(90deg, rgba(255,255,255,0.03) 1px, transparent 1px);
    background-size: 50px 50px;
}
```

## Troubleshooting

| Problem | Fix |
|---------|-----|
| Fonts not loading | Check Google Fonts URL; ensure font names match in CSS |
| Animations not triggering | Verify Intersection Observer is running; check `.visible` class is being added |
| Scroll snap not working | Ensure `scroll-snap-type: y mandatory` on html; each slide needs `scroll-snap-align: start` |
| Mobile issues | Disable heavy effects at 768px breakpoint; test touch events |
| Performance issues | Use `will-change` sparingly; prefer `transform`/`opacity` animations |
