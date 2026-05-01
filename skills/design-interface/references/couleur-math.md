# 13 — Mathematics & Color

Source: Math for Web Design — Paul McFedries

---

## Contrast Ratio Calculation (WCAG)

### Official Formula

```
CR = (L1 + 0.05) / (L2 + 0.05)
```

- `L1`: relative luminance of the **lighter** color
- `L2`: relative luminance of the **darker** color
- `CR`: contrast ratio (1:1 = no contrast, 21:1 = black on white)

### Relative Luminance Calculation

```javascript
function getLuminance(r, g, b) {
  // Normalize 0-255 → 0-1
  const [rs, gs, bs] = [r, g, b].map(c => {
    c = c / 255;
    return c <= 0.03928
      ? c / 12.92
      : Math.pow((c + 0.055) / 1.055, 2.4);
  });
  // WCAG Formula
  return 0.2126 * rs + 0.7152 * gs + 0.0722 * bs;
}

function contrastRatio(color1RGB, color2RGB) {
  const L1 = getLuminance(...color1RGB);
  const L2 = getLuminance(...color2RGB);
  const lighter = Math.max(L1, L2);
  const darker  = Math.min(L1, L2);
  return +((lighter + 0.05) / (darker + 0.05)).toFixed(2);
}

// Example
contrastRatio([255, 255, 255], [0, 0, 0]);     // → 21
contrastRatio([255, 255, 255], [100, 100, 100]); // → 5.9 (AA ✓)
```

### WCAG 2.1 Thresholds

| Level | Normal Text | Large Text (≥18px or bold ≥14px) | UI Components |
|--------|-------------|-----------------------------------|---------------|
| AA     | **4.5:1**   | **3:1**                           | **3:1**       |
| AAA    | 7:1         | 4.5:1                             | N/A           |

---

## HSL Palette Generation: Algorithm

### 3 Anchors + Interpolation Method

```javascript
function generatePalette(hue, saturation) {
  // 3 anchors: very light (100), base (500), very dark (900)
  const anchors = {
    100: { s: saturation * 0.4, l: 94 },
    500: { s: saturation,       l: 50 },
    900: { s: saturation * 0.6, l: 15 }
  };

  // Linear interpolation between anchors
  function interpolate(step) {
    if (step <= 500) {
      const t = (step - 100) / 400;
      return {
        s: anchors[100].s + (anchors[500].s - anchors[100].s) * t,
        l: anchors[100].l + (anchors[500].l - anchors[100].l) * t
      };
    } else {
      const t = (step - 500) / 400;
      return {
        s: anchors[500].s + (anchors[900].s - anchors[500].s) * t,
        l: anchors[500].l + (anchors[900].l - anchors[500].l) * t
      };
    }
  }

  const steps = [50, 100, 200, 300, 400, 500, 600, 700, 800, 900, 950];
  return steps.reduce((palette, step) => {
    const { s, l } = step === 50
      ? { s: saturation * 0.2, l: 97 }
      : step === 950
      ? { s: saturation * 0.5, l: 8 }
      : interpolate(step);
    palette[step] = `hsl(${hue}, ${s.toFixed(1)}%, ${l.toFixed(1)}%)`;
    return palette;
  }, {});
}

// Example: blue palette
const blue = generatePalette(214, 70);
```

---

## Hue Rotation for Depth

Standard HSL has a flaw: at equal lightness, blue seems darker than yellow. To maintain **perceived vibrancy** when darkening or lightening:

### Rotation Rule

```
To lighten → rotate hue towards 60° (yellow), 180° (cyan), or 300° (magenta)
To darken → rotate hue towards 0° (red), 120° (green), or 240° (blue)
```

Never exceed **20-30°** of rotation or the color will look like a different color.

```javascript
function shiftHue(baseHue, lightness, targetLightness) {
  const diff = targetLightness - lightness;
  // Hue shift proportional to lightness variation
  const hueShift = diff > 0 ? -diff * 0.5 : -diff * 0.3;
  return ((baseHue + hueShift) % 360 + 360) % 360;
}
```

---

## OKLCH: The Superior Model

HSL has a fundamental limitation: it is not **perceptually uniform**. Two colors with the same HSL lightness can have very different perceived brightness.

**OKLCH** (`oklch(L C H)`) solves this:
- `L`: perceived lightness (0-1, linear)
- `C`: chroma / saturation (0+)
- `H`: hue (0-360°)

```css
/* HSL — blue and yellow look different at same lightness */
hsl(240, 80%, 50%)  /* blue — looks dark */
hsl(60,  80%, 50%)  /* yellow — looks bright */

/* OKLCH — perceived brightness actually identical */
oklch(0.55 0.2 264)  /* blue */
oklch(0.85 0.18 100) /* yellow — L different because yellow is intrinsically light */
```

### Practical Recommendation
- Use **HSL** for tokens and palette generation (universal compatibility)
- Use **OKLCH** for fine adjustments of perceived contrast (modern browsers)

---

## State Variant Calculation (hover/active/disabled)

### HSL Formulas

```javascript
function stateVariants(h, s, l) {
  return {
    default:  `hsl(${h}, ${s}%, ${l}%)`,
    hover:    `hsl(${h}, ${s}%, ${Math.max(0, l - 8)}%)`,
    active:   `hsl(${h}, ${s}%, ${Math.max(0, l - 15)}%)`,
    focus:    `hsl(${h}, ${s}%, ${l}%)`,  // same color + ring
    disabled: `hsl(${h}, ${Math.round(s * 0.4)}%, ${l + 20}%)`,
  };
}

// Example: blue button hsl(214, 70%, 50%)
stateVariants(214, 70, 50);
// default:  hsl(214, 70%, 50%)
// hover:    hsl(214, 70%, 42%)
// active:   hsl(214, 70%, 35%)
// disabled: hsl(214, 28%, 70%)
```

### In CSS with relative colors (modern)

```css
:root {
  --btn-bg: hsl(214, 70%, 50%);
}

.btn:hover  { background: hsl(from var(--btn-bg) h s calc(l - 8)); }
.btn:active { background: hsl(from var(--btn-bg) h s calc(l - 15)); }
```

---

## Dark Mode: HSL Mirroring

For a consistent dark mode, do not simply invert colors. Use a shift strategy:

### Mirroring Formula

```javascript
function darkModeVariant(h, s, l) {
  return {
    // Shift hue by 15-30° for a more atmospheric look
    hue: h + 15,
    // Reduce saturation by 10-30%
    saturation: Math.round(s * 0.75),
    // Invert lightness around center (50%)
    lightness: 100 - l
  };
}
```

### Practical Application

```css
:root {
  /* Light mode */
  --gray-50:  hsl(220, 20%, 98%);
  --gray-900: hsl(220, 16%, 10%);
  --color-bg: var(--gray-50);
  --color-text: var(--gray-900);
}

[data-theme="dark"] {
  /* Dark mode — not a brutal inversion */
  --color-bg:   hsl(235, 12%, 10%);  /* shifted hue, reduced saturation */
  --color-text: hsl(220, 15%, 90%);  /* not pure white */

  /* Brand colors desaturate slightly */
  --color-brand: hsl(214, 55%, 60%); /* saturation -15%, lightness +10% */
}
```
