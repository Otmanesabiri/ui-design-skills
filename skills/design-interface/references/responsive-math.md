# 12 — Fluid CSS & Responsive Math

Source: Math for Web Design — Paul McFedries

---

## `clamp()`: The Fundamental Formula

```css
clamp(MIN, PREFERRED, MAX)
```

Mathematical equivalent: `max(MIN, min(PREFERRED, MAX))`

The browser returns:
- `MIN` if `PREFERRED < MIN`
- `PREFERRED` if `MIN ≤ PREFERRED ≤ MAX`
- `MAX` if `PREFERRED > MAX`

---

## Calculating Fluid `preferred` Value

For a value to be **exactly proportional** between two breakpoints:

### Formula

```
slope = (maxValue - minValue) / (maxVW - minVW)
preferred = slope × 100vw + intercept
intercept = minValue - slope × minVW
```

### Concrete Example: Fluid font-size from 16px to 24px between 320px and 1280px

```
slope = (24 - 16) / (1280 - 320) = 8 / 960 = 0.00833
preferred = 0.00833 × 100vw = 0.833vw
intercept = 16 - 0.00833 × 320 = 16 - 2.67 = 13.33px

→ clamp(16px, 13.33px + 0.833vw, 24px)
```

In CSS:
```css
font-size: clamp(1rem, 0.833rem + 0.833vw, 1.5rem);
```

### JS Calculation Tool

```javascript
function fluidValue(minVal, maxVal, minVW, maxVW) {
  const slope = (maxVal - minVal) / (maxVW - minVW);
  const intercept = minVal - slope * minVW;
  return {
    clamp: `clamp(${minVal}px, ${intercept.toFixed(4)}px + ${(slope * 100).toFixed(4)}vw, ${maxVal}px)`,
    slope,
    intercept
  };
}

// Usage
fluidValue(16, 24, 320, 1280);
// → clamp(16px, 13.3333px + 0.8333vw, 24px)
```

---

## Full Fluid Type Scale

```css
:root {
  /* xs : 12px → 14px */
  --text-xs: clamp(0.75rem, 0.7083rem + 0.2083vw, 0.875rem);

  /* sm : 14px → 16px */
  --text-sm: clamp(0.875rem, 0.8333rem + 0.2083vw, 1rem);

  /* base : 16px → 18px */
  --text-base: clamp(1rem, 0.9583rem + 0.2083vw, 1.125rem);

  /* lg : 18px → 22px */
  --text-lg: clamp(1.125rem, 1.0417rem + 0.4167vw, 1.375rem);

  /* xl : 20px → 26px */
  --text-xl: clamp(1.25rem, 1.125rem + 0.625vw, 1.625rem);

  /* 2xl : 24px → 36px */
  --text-2xl: clamp(1.5rem, 1.25rem + 1.25vw, 2.25rem);

  /* 3xl : 30px → 48px */
  --text-3xl: clamp(1.875rem, 1.5rem + 1.875vw, 3rem);

  /* 4xl : 36px → 64px */
  --text-4xl: clamp(2.25rem, 1.6667rem + 2.9167vw, 4rem);

  /* 5xl : 48px → 80px */
  --text-5xl: clamp(3rem, 2.3333rem + 3.3333vw, 5rem);
}
```

---

## Fluid Spacing Tokens

```css
:root {
  /* space-1 : 4px → 8px */
  --space-1: clamp(0.25rem, 0.1667rem + 0.4167vw, 0.5rem);

  /* space-2 : 8px → 12px */
  --space-2: clamp(0.5rem, 0.4167rem + 0.4167vw, 0.75rem);

  /* space-4 : 16px → 24px */
  --space-4: clamp(1rem, 0.8333rem + 0.8333vw, 1.5rem);

  /* space-6 : 24px → 40px */
  --space-6: clamp(1.5rem, 1.1667rem + 1.6667vw, 2.5rem);

  /* space-8 : 32px → 64px */
  --space-8: clamp(2rem, 1.3333rem + 3.3333vw, 4rem);

  /* space-12 : 48px → 96px */
  --space-12: clamp(3rem, 2rem + 5vw, 6rem);

  /* space-16 : 64px → 128px */
  --space-16: clamp(4rem, 2.6667rem + 6.6667vw, 8rem);
}
```

---

## `min()` and `max()`: Use Cases

### `min()` — Smallest Value
```css
/* Width never exceeding 600px but can be smaller */
.container {
  width: min(600px, 100%);
}

/* Padding that doesn't exceed 5% of the width */
.section {
  padding-inline: min(5%, 48px);
}
```

### `max()` — Largest Value
```css
/* Font-size never below 16px */
p {
  font-size: max(16px, 1.5vw);
}

/* Guaranteed minimum height */
.hero {
  min-height: max(400px, 50vh);
}
```

---

## Proportional Grids Without Breakpoints

### Auto-Adaptive Grid Formula

```css
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(MIN, 1fr));
}
```

The browser calculates the number of columns:
```
n = floor((containerWidth - sumGaps) / MIN)
```

### Concrete Examples

```css
/* Card grid: 3 columns on desktop, 1 on mobile */
.cards-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: var(--space-6);
}

/* Tag grid: adapts to content */
.tags-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(120px, 1fr));
  gap: var(--space-2);
}
```

### Golden Ratio Grid

```css
/* Sidebar + Content (1:1.618 ratio) */
.golden-layout {
  display: grid;
  grid-template-columns: 1fr 1.618fr;
  gap: var(--space-8);
}

/* Responsive: stack on mobile */
@media (max-width: 768px) {
  .golden-layout {
    grid-template-columns: 1fr;
  }
}
```

### `fr` Column Grid: Calculation

For `grid-template-columns: 1fr 2fr 1fr` with a 960px container and two 24px gaps:

```
Remaining space = 960 - (2 × 24) = 912px
Total fr = 1 + 2 + 1 = 4fr
1fr = 912 / 4 = 228px
2fr = 456px
```

---

## `calc()`: Algebra in CSS

### Use Cases

```css
/* Width = 100% minus a fixed sidebar */
.main-content {
  width: calc(100% - 280px);
}

/* Padding accounting for scrollbar */
.modal {
  padding-right: calc(var(--space-8) + var(--scrollbar-width, 0px));
}

/* Intermediate font-size between two system values */
.special-text {
  font-size: calc((var(--text-lg) + var(--text-xl)) / 2);
}

/* Fullscreen height minus header */
.hero {
  min-height: calc(100vh - 64px);
  min-height: calc(100dvh - 64px); /* dynamic viewport height */
}
```

### Precautions

```css
/* ✓ Good: compatible units in the operation */
width: calc(100% - 48px);

/* ✗ Bad: division by a value with unit */
font-size: calc(32px / 2px);  /* invalid */
font-size: calc(32px / 2);    /* valid → 16px */
```

---

## Vertical Percentages: The Trap

In CSS, `margin` and `padding` in percentage (even `margin-top`, `padding-bottom`) are calculated relative to the **parent width**, not height.

```css
/* padding-top: 56.25% = 16:9 ratio (100/16×9) */
.video-wrapper {
  position: relative;
  width: 100%;
  padding-top: 56.25%; /* 9/16 = 0.5625 */
}

.video-wrapper > iframe {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
}
```

This maintains constant aspect ratios regardless of the container width.
