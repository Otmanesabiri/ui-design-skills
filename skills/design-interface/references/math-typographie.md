# 11 — Mathematics & Typography

Source: Math for Web Design — Paul McFedries

---

## Type Scale: Fundamental Formula

Each level of a typographic scale is calculated by:

```
Size = Base × Ratio^n
```

- `Base`: reference size (16px recommended)
- `Ratio`: the chosen multiplier
- `n`: the level (positive = larger, negative = smaller)

### Example with 16px base and 1.25 ratio (Major Third)

```
n = -2 → 16 × 1.25^-2 = 10.24px  → ~10px  (xs)
n = -1 → 16 × 1.25^-1 = 12.8px   → ~13px  (sm)
n =  0 → 16 × 1.25^0  = 16px     → 16px   (base)
n =  1 → 16 × 1.25^1  = 20px     → 20px   (lg)
n =  2 → 16 × 1.25^2  = 25px     → 25px   (xl)
n =  3 → 16 × 1.25^3  = 31.25px  → 31px   (2xl)
n =  4 → 16 × 1.25^4  = 39.06px  → 39px   (3xl)
n =  5 → 16 × 1.25^5  = 48.83px  → 49px   (4xl)
```

---

## Available Ratios and Their Usages

| Ratio | Name | Value | Recommended Usage |
|-------|-----|--------|-----------------|
| Minor Second | Minor Second | 1.067 | Very dense interfaces, little variation |
| Major Second | Major Second | 1.125 | Compact UI, dashboards |
| Minor Third | Minor Third | 1.200 | **Standard UI interfaces** |
| Major Third | Major Third | 1.250 | **Good balance — recommended** |
| Perfect Fourth | Perfect Fourth | 1.333 | Marketing sites, landing pages |
| Augmented Fourth | Augmented Fourth | 1.414 | Expressive titles |
| Perfect Fifth | Perfect Fifth | 1.500 | Display, large screens |
| Golden Ratio | Golden Ratio | 1.618 | Very large gap between levels |

### JS Calculation Tool

```javascript
function typeScale(base, ratio, steps) {
  return steps.map(n => ({
    step: n,
    size: +(base * Math.pow(ratio, n)).toFixed(2)
  }));
}

// Example: Major Third, 16px base, levels -2 to +5
const scale = typeScale(16, 1.25, [-2, -1, 0, 1, 2, 3, 4, 5]);
```

---

## Golden Ratio (1.618)

### In Typography

The 1.618 ratio between two sizes creates a naturally harmonious visual relationship.

```css
/* Body text → H1 Title */
--text-base: 16px;
--text-h1: calc(16px * 1.618 * 1.618); /* ~41.9px */

/* Or applied progressively */
--text-base: 1rem;     /* 16px */
--text-lg: 1.618rem;   /* 25.9px */
--text-xl: 2.618rem;   /* 41.9px */
```

### In Layout

```css
/* Sidebar / Main Content */
.layout {
  display: grid;
  grid-template-columns: 1fr 1.618fr;
  /* Sidebar ≈ 38% | Content ≈ 62% */
}

/* Equivalent in 12 columns: sidebar 4-5 col, content 7-8 col */
```

---

## Line-height: The Two Mathematical Rules

### Rule 1: Inversely Proportional to Size
The larger the font, the less additional line spacing is needed.

```
line-height ↓ when font-size ↑
```

| Size | Recommended Line-height |
|--------|----------------------|
| 12-14px | 1.6 – 1.8 |
| 16-18px | 1.5 – 1.6 |
| 20-24px | 1.4 – 1.5 |
| 30-36px | 1.2 – 1.35 |
| 48px+   | 1.0 – 1.2 |

### Rule 2: Proportional to Line Length
The wider the column, the higher the line-height must be to help the eye return to the next line.

```
line-height ↑ when line-length ↑
```

| Column Width | Recommended Line-height |
|--------------------|----------------------|
| < 45 characters | 1.3 – 1.4 |
| 45-65 characters | 1.5 – 1.6 |
| 65-80 characters | 1.6 – 1.75 |
| > 80 characters | 1.75 – 2.0 |

---

## Vertical Rhythm (Baseline Grid)

### Principle
All page elements align to a grid of imaginary lines spaced at a fixed value. This creates a consistent visual rhythm.

### Calculation

```
Baseline unit = body text line-height in px

Example: 16px × 1.5 = 24px → baseline unit = 24px
```

All vertical spacings (margin, padding, gap) are multiples of this value:
```css
:root {
  --baseline: 24px;  /* 16px × 1.5 */

  --space-half:  calc(var(--baseline) * 0.5);  /* 12px */
  --space-1:     var(--baseline);               /* 24px */
  --space-2:     calc(var(--baseline) * 2);     /* 48px */
  --space-3:     calc(var(--baseline) * 3);     /* 72px */
  --space-4:     calc(var(--baseline) * 4);     /* 96px */
}
```

### Baseline Alignment in Code

```css
/* Align by baseline, not by center */
.mixed-sizes {
  display: flex;
  align-items: baseline;  /* never "center" for mixed text */
}
```
