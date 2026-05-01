# 04 — Typography

Sources: Refactoring UI ch.5 (Designing Text) · Practical UI ch.5 (Typography)

> **Note:** This file describes the principles of typographic choices and standard scales. To generate a custom mathematical type scale (Type Scale ratio) or manage vertical rhythm (Baseline Grid), see `math-typographie.md`. To make these fonts fluid, see `responsive-math.md`.

---

## Size System (Type Scale)

### Fundamental Rule
Never use arbitrary sizes. Define a fixed scale in advance and only choose from this scale.

### Base: 16px
16px is the default for browsers. It divides well (÷2=8, ÷4=4) and serves as a natural starting point.

### Recommended Scale (in px / rem)
```
12px  / 0.75rem   → tiny labels, captions
14px  / 0.875rem  → small text, helper text
16px  / 1rem      → body text (base)
18px  / 1.125rem  → slightly large body
20px  / 1.25rem   → intro, lead paragraph
24px  / 1.5rem    → H4, subheadings
30px  / 1.875rem  → H3
36px  / 2.25rem   → H2
48px  / 3rem      → H1 desktop
60px  / 3.75rem   → Hero title
72px  / 4.5rem    → Display
```

### Units: px or rem, never em
`em` are relative to the font size of the parent element. In nested elements, the calculated size often falls outside the defined scale.

```css
/* BAD - nested em */
.parent { font-size: 1.25em; }  /* 20px */
.child  { font-size: 0.875em; } /* 17.5px — not in the scale! */

/* GOOD - rem */
.parent { font-size: 1.25rem; } /* 20px */
.child  { font-size: 0.875rem; }/* 14px — in the scale */
```

---

## Font Family

### Basic Rule
- **1 sans-serif font** for the general interface
- Optionally **1 serif font** for titles (emotion, personality)
- Maximum **2 families** in the same interface

### Choosing a Good Sans-Serif Font
Characteristics of a good UI font:
- Generous x-height (readability at small sizes)
- Open forms (the "c", the "g" don't close too much)
- Tabular figures available (for data tables)

**Proven Fonts:**
- Inter (free, excellent at small sizes)
- SF Pro (Apple, native macOS/iOS)
- Segoe UI (Microsoft, native Windows)
- Roboto (Google, native Android)

### Avoid
- Decorative fonts for body text
- Condensed fonts for reading text
- Too light fonts (thin) for functional text

---

## Line-height

### Rule: Line-height Proportional to Size
The larger the text, the **smaller** the line-height should be. Absolute space between lines increases anyway with font size.

| Context | Recommended Line-height |
|---|---|
| Body text (16-18px) | 1.5 – 1.6 (150-160%) |
| Intermediate text (20-24px) | 1.4 – 1.5 |
| Subheadings (24-36px) | 1.3 – 1.4 |
| Headings (36px+) | 1.1 – 1.3 |
| Short labels, one line | 1.0 – 1.2 |

---

## Line Length

### Ideal Zone
**45 to 75 characters** per line for reading text.

In practice, this corresponds to about `60-75ch` in CSS:
```css
.prose {
  max-width: 65ch;
}
```

**Too short** (< 45 char): line breaks break the reading rhythm.
**Too long** (> 75 char): hard to find the beginning of the next line.

---

## Alignment

### General Rule: Left-aligned Text
For all languages read left-to-right, left alignment is the default for body text.

### Center: Only for Short Independent Blocks
Center short titles, short CTAs, headlines — never paragraphs.

```
✓ Center: a standalone H1 title, a slogan, a section label
✗ Center: more than 2-3 consecutive lines of text
```

If a centered block seems too long, rewrite the content to shorten it rather than changing the alignment.

### Right-align Numbers in Tables
Decimals stay vertically aligned, making comparison easier.

### Baseline Alignment for Mixed Sizes
When two elements of different sizes are side by side, align them by the **baseline**, not the center.

```css
.mixed-size-container {
  display: flex;
  align-items: baseline;  /* not center */
}
```

---

## Letter-spacing

### Basic Rule: Trust the Font Designer
Do not modify default letter-spacing except in two cases:

**1. Headings in large fonts → reduce letter-spacing**
Fonts designed for body text (wide spacing) seem too spaced out at large sizes.
```css
h1 { letter-spacing: -0.025em; }
h2 { letter-spacing: -0.02em; }
```

**2. Uppercase text → increase letter-spacing**
Uppercase letters all have the same height, making them hard to read without extra spacing.
```css
.label-uppercase {
  text-transform: uppercase;
  letter-spacing: 0.05em;
  font-size: 12px;
  font-weight: 600;
}
```

---

## Font-weight

### Recommended Weight Palette for UI
```
400 (Regular)  → body text, data values
500 (Medium)   → labels, navigation
600 (Semibold) → subheadings, important elements
700 (Bold)     → headings, critical data
```

### Avoid
- `300` (Light) for functional text — hard to read on screen
- `900` (Black) except for marketing display

---

## Uppercase: Restricted Usage

### When to Use Uppercase
Only for **short labels** (2-4 words maximum):
- Categories, sections
- Metadata labels
- Secondary navigation

### Never Uppercase for
- Body text
- Long titles
- Buttons (unless specific convention)
- Entire sentences

### Correct Formatting for Uppercase
```css
.uppercase-label {
  text-transform: uppercase;
  letter-spacing: 0.06em;
  font-size: 11px;
  font-weight: 600;
  color: hsl(220, 10%, 55%);  /* secondary, not primary */
}
```

---

## Links: Not Always in Color

In a standard block of text → links must stand out (color + underline).

In an interface where almost everything is a link (navigation, dashboard) → use more subtle treatments:
- Higher font-weight
- Slightly darker color
- Underline visible only on hover

This prevents the entire interface from being invaded by blue.