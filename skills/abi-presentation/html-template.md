# HTML Presentation Template

Reference architecture for generating slide presentations. Every presentation follows this structure.

## Base HTML Structure

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Presentation Title</title>

    <!-- Acumen BI: always DM Sans + DM Mono -->
    <link href="https://fonts.googleapis.com/css2?family=DM+Sans:ital,wght@0,300;0,400;0,500;0,600;1,300&family=DM+Mono:wght@400&display=swap" rel="stylesheet" />

    <style>
      /* ===========================================
           CSS CUSTOM PROPERTIES (THEME)
           Change :root variables to restyle the deck
           =========================================== */
      :root {
        /* Colors — from chosen Acumen brand preset */
        --bg-primary:   #061626;
        --accent-green: #6A9E39;
        --accent-teal:  #1F798C;
        --accent-brass: #B5892A;
        --accent-rose:  #8C5470;
        --text-heading: #ffffff;
        --text-sub:     rgba(255,255,255,0.55);
        --text-body:    rgba(255,255,255,0.40);
        --text-label:   #1F798C;
        --card-bg:      rgba(255,255,255,0.05);
        --card-border:  rgba(255,255,255,0.07);

        /* Typography — MUST use clamp() */
        --font-display: 'DM Sans', sans-serif;
        --font-mono:    'DM Mono', monospace;
        --title-size:   clamp(2rem, 6vw, 5rem);
        --h2-size:      clamp(1.4rem, 3.5vw, 2.8rem);
        --body-size:    clamp(0.75rem, 1.4vw, 1.05rem);
        --label-size:   clamp(0.58rem, 0.85vw, 0.72rem);

        /* Spacing — MUST use clamp() */
        --slide-padding: clamp(1.5rem, 5vw, 5rem);
        --content-gap:   clamp(0.75rem, 2vw, 2rem);

        /* Animation */
        --ease-out-expo: cubic-bezier(0.16, 1, 0.3, 1);
        --duration-normal: 0.65s;
      }

      /* ===========================================
           BASE STYLES
           =========================================== */
      *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

      /* --- PASTE viewport-base.css CONTENTS HERE --- */

      /* === GREEN TOP BAR (non-negotiable on every slide) === */
      .brand-bar {
        position: absolute;
        top: 0; left: 0; right: 0;
        height: 3px;
        background: var(--accent-green);
        z-index: 10;
      }

      /* ===========================================
           ANIMATIONS
           Trigger via .visible class (added by JS on scroll)
           =========================================== */
      .reveal {
        opacity: 0;
        transform: translateY(22px);
        transition:
          opacity var(--duration-normal) var(--ease-out-expo),
          transform var(--duration-normal) var(--ease-out-expo);
      }

      .slide.visible .reveal {
        opacity: 1;
        transform: translateY(0);
      }

      /* Stagger children for sequential reveal */
      .slide.visible .reveal:nth-child(1) { transition-delay: 0.08s; }
      .slide.visible .reveal:nth-child(2) { transition-delay: 0.18s; }
      .slide.visible .reveal:nth-child(3) { transition-delay: 0.28s; }
      .slide.visible .reveal:nth-child(4) { transition-delay: 0.38s; }
      .slide.visible .reveal:nth-child(5) { transition-delay: 0.46s; }
      .slide.visible .reveal:nth-child(6) { transition-delay: 0.54s; }

      /* ... preset-specific styles ... */
    </style>
  </head>
  <body>
    <!-- Progress bar -->
    <div class="progress-bar" id="progressBar"></div>

    <!-- Navigation dots -->
    <nav class="nav-dots" id="navDots"></nav>

    <!-- Slides -->
    <section class="slide" data-index="0">
      <div class="brand-bar"></div>
      <!-- slide content -->
    </section>

    <!-- More slides... -->

    <script>
      /* === SLIDE PRESENTATION CONTROLLER === */
      class SlidePresentation {
        constructor() {
          this.slides = Array.from(document.querySelectorAll('.slide'));
          this.currentIndex = 0;
          this.touchStartY = 0;
          this.progressBar = document.getElementById('progressBar');
          this.navDotsContainer = document.getElementById('navDots');
          this.buildNavDots();
          this.setupIntersectionObserver();
          this.setupKeyboard();
          this.setupTouch();
          this.setupWheel();
          this.updateProgress(0);
        }

        buildNavDots() {
          this.navDotsContainer.innerHTML = ''; // Always clear first
          this.slides.forEach((_, i) => {
            const btn = document.createElement('button');
            btn.className = 'nav-dot' + (i === 0 ? ' active' : '');
            btn.setAttribute('aria-label', `Go to slide ${i + 1}`);
            btn.addEventListener('click', () => this.goTo(i));
            this.navDotsContainer.appendChild(btn);
          });
        }

        setupIntersectionObserver() {
          const obs = new IntersectionObserver(
            (entries) => {
              entries.forEach(entry => {
                if (entry.isIntersecting) {
                  entry.target.classList.add('visible');
                  const idx = parseInt(entry.target.dataset.index);
                  this.currentIndex = idx;
                  this.updateProgress(idx);
                  this.updateDots(idx);
                }
              });
            },
            { threshold: 0.55 }
          );
          this.slides.forEach(slide => obs.observe(slide));
        }

        setupKeyboard() {
          document.addEventListener('keydown', e => {
            switch (e.key) {
              case 'ArrowDown': case 'ArrowRight': case ' ':
                e.preventDefault(); this.next(); break;
              case 'ArrowUp': case 'ArrowLeft':
                e.preventDefault(); this.prev(); break;
              case 'PageDown': e.preventDefault(); this.next(); break;
              case 'PageUp':   e.preventDefault(); this.prev(); break;
              case 'Home': e.preventDefault(); this.goTo(0); break;
              case 'End':  e.preventDefault(); this.goTo(this.slides.length - 1); break;
            }
          });
        }

        setupTouch() {
          document.addEventListener('touchstart', e => {
            this.touchStartY = e.touches[0].clientY;
          }, { passive: true });
          document.addEventListener('touchend', e => {
            const delta = this.touchStartY - e.changedTouches[0].clientY;
            if (Math.abs(delta) > 40) delta > 0 ? this.next() : this.prev();
          }, { passive: true });
        }

        setupWheel() {
          let last = 0;
          document.addEventListener('wheel', e => {
            e.preventDefault();
            const now = Date.now();
            if (now - last < 800) return;
            last = now;
            e.deltaY > 0 ? this.next() : this.prev();
          }, { passive: false });
        }

        next() { if (this.currentIndex < this.slides.length - 1) this.goTo(this.currentIndex + 1); }
        prev() { if (this.currentIndex > 0) this.goTo(this.currentIndex - 1); }
        goTo(i) { this.slides[i].scrollIntoView({ behavior: 'smooth' }); }

        updateProgress(i) {
          const pct = this.slides.length > 1 ? (i / (this.slides.length - 1)) * 100 : 100;
          this.progressBar.style.width = pct + '%';
        }
        updateDots(i) {
          this.navDotsContainer.querySelectorAll('.nav-dot').forEach((d, idx) => {
            d.classList.toggle('active', idx === i);
          });
        }
      }
      new SlidePresentation();
    </script>
  </body>
</html>
```

## Required JavaScript Features

Every presentation must include:

1. **SlidePresentation Class** — keyboard nav, touch/swipe, mouse wheel, progress bar, nav dots
2. **Intersection Observer** — adds `.visible` to trigger `.reveal` animations
3. **Inline Editing** (only if user opted in — skip entirely if they said No)

## Inline Editing Implementation (Opt-In Only)

**Do NOT use CSS `~` sibling selector for hover-based show/hide.** Use JS with 400ms delay timeout.

```javascript
// Hotzone hover with 400ms grace period
let hideTimeout = null;
hotzone.addEventListener('mouseenter', () => { clearTimeout(hideTimeout); editToggle.classList.add('show'); });
hotzone.addEventListener('mouseleave', () => {
  hideTimeout = setTimeout(() => { if (!editor.isActive) editToggle.classList.remove('show'); }, 400);
});
```

**CRITICAL: `exportFile()` must strip edit state before capturing outerHTML** — otherwise the saved file opens stuck in edit mode.

## Code Quality

- Semantic HTML (`<section>`, `<nav>`)
- Every section has a `/* === SECTION NAME === */` comment block
- ARIA labels on interactive elements
- `prefers-reduced-motion` support (included in viewport-base.css)
