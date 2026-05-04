# Performance & Design (Core Web Vitals)

Sources: web.dev · Google Lighthouse · WCAG 2.2 · Doherty Threshold

> **Agent Instruction:** Load this file ONLY for performance optimization tasks. For CSS values, always reference `references/tokens.md`. For skeleton screen CSS, see `references/composants.md` (Loading State section). For animation performance, see `references/animations-math.md`.

---

## Why Performance Is a Design Decision

| Design Decision | Performance Impact |
|----------------|-------------------|
| Hero image (unoptimized 2MB JPEG) | LCP delayed by 2-4 seconds |
| 3 Google Fonts loaded | +300KB, FOUT/FOIT flash |
| 15 box-shadows on dashboard cards | Paint time doubled |
| CSS animation on scroll (no will-change) | Jank, dropped frames |
| 200-row table rendered at once | Main thread blocked 500ms+ |

---

## Core Web Vitals

### 1. LCP — Largest Contentful Paint (< 2.5s)

```
[ ] Hero image uses <img> with width/height (reserve space)
[ ] Modern formats: WebP (fallback JPEG) or AVIF
[ ] Above-the-fold images: eager load, preload in <head>
[ ] Below-the-fold images: loading="lazy"
[ ] Hero text readable without custom font
```

```css
.hero-image {
  aspect-ratio: 16 / 9;
  width: 100%;
  object-fit: cover;
  background: var(--gray-200);
}
```

### 2. CLS — Cumulative Layout Shift (< 0.1)

| Element | Problem | Fix |
|---------|---------|-----|
| Images without dimensions | Content shifts | `width` + `height` attributes |
| Web fonts loading late | Text resizes | `font-display: swap` + size-adjust |
| Dynamic banners | Push content down | Fixed/overlay positioning |
| Lazy content | Sudden appearance | Skeleton placeholder |

### 3. INP — Interaction to Next Paint (< 200ms)

```
[ ] Click handlers must not block main thread > 50ms
[ ] Use CSS transitions over JS animations where possible
[ ] Debounce search/filter inputs (300ms minimum)
[ ] Virtualize long lists (> 100 items)
[ ] Use requestAnimationFrame for visual updates
```

---

## Font Performance Budget

```
Maximum: 2 font families, 4 weights total, < 150KB combined

Setup:
  - 1 sans-serif for UI (Inter, Roboto, or system-ui)
  - Weights: 400 (body), 500 (labels), 600 (headings), 700 (emphasis)
  - Format: WOFF2 only
```

```css
@font-face {
  font-family: 'Inter';
  src: url('/fonts/inter-var.woff2') format('woff2');
  font-weight: 100 900;
  font-display: swap;
  unicode-range: U+0000-00FF;
}

/* System Font Stack (zero network cost for checkout pages) */
:root {
  --font-system: -apple-system, BlinkMacSystemFont, 'Segoe UI',
                 Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
}
```

---

## Image Optimization

| Content | Format | Quality |
|---------|--------|---------|
| Photographs | WebP (fallback JPEG) | 75-85% |
| Icons, logos | SVG (inline) | N/A |
| Screenshots | WebP or PNG | 85-90% |

```html
<img
  src="hero-800.webp"
  srcset="hero-400.webp 400w, hero-800.webp 800w, hero-1200.webp 1200w"
  sizes="(max-width: 768px) 100vw, 50vw"
  alt="Dashboard showing revenue metrics"
  width="1600" height="900"
  loading="lazy" decoding="async"
/>
```

### Placeholder Strategies

```css
/* Dominant Color */
.image-wrapper {
  background: hsl(220, 15%, 90%);
  aspect-ratio: 16 / 9;
}

/* Blur-up (LQIP) */
.image-wrapper {
  background-image: url('hero-tiny.webp');
  background-size: cover;
  filter: blur(20px);
  transition: filter 300ms var(--ease-out);
}
.image-wrapper.loaded { filter: blur(0); }
```

---

## Animation Performance

### GPU-Accelerated (Cheap — use these)

```css
transform: translateX() / translateY() / scale() / rotate();
opacity: 0..1;
filter: blur() / brightness();

.animated-element { will-change: transform, opacity; }
```

### Expensive (Avoid animating)

```css
❌ width, height, top, left, margin, padding, border-width, font-size
✅ Use transform: scale() instead of width/height
✅ Use transform: translate() instead of top/left
```

### 60fps Rule
Frame budget = 16.67ms. If logic > 10ms → use requestAnimationFrame or Web Worker.

---

## Skeleton Screens

> **Cross-reference:** Full skeleton CSS is in `references/composants.md` (Loading State section). Do not duplicate it here.

| Load Time | Strategy |
|-----------|----------|
| < 300ms | Nothing (too fast to matter) |
| 300ms - 1s | Subtle spinner |
| 1s - 3s | Skeleton screen |
| > 3s | Skeleton + progress text |

**Rules:** Skeleton must match final content shape exactly. Animate with shimmer (not pulse). Respect `prefers-reduced-motion`. Remove with fade (opacity 300ms).

---

## Virtualization

```
< 50 items   → Render all
50-200 items  → Consider virtualizing
> 200 items   → Must virtualize
> 1000 items  → Virtualize + server-side pagination
```

---

## Checklist

```
Fonts
[ ] Max 2 families, WOFF2 only, font-display: swap
[ ] Critical font preloaded, total < 150KB

Images
[ ] WebP/AVIF, width+height on every <img>
[ ] loading="lazy" below-the-fold, srcset+sizes used

Layout Stability
[ ] No content inserted above existing content
[ ] Skeleton dimensions match final content

Animation
[ ] Only transform + opacity animated
[ ] prefers-reduced-motion respected

Rendering
[ ] Lists > 200 items virtualized
[ ] Input handlers debounced (300ms)
```
