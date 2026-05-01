# 05 — Spacing, Layout & Depth

Sources: Refactoring UI ch.3 (Spacing & Layout) · Practical UI ch.4 (Layout and Spacing)

> **Note:** This file describes the static spacing system and grid theory. To make this spacing system fluid with `clamp()` and create mathematical grids without media queries, see `responsive-math.md`.

---

## Spacing System

### Fundamental Rule
Define a set of predefined values. Never invent an arbitrary value.

### Recommended Scale (4px base)
```
4px   → micro (separator for icon and label, internal gap)
8px   → xs (compact internal padding)
12px  → sm (small button padding, gap between close elements)
16px  → md (standard padding, gap between form fields)
24px  → lg (card padding, separation of related sections)
32px  → xl (separation of blocks)
48px  → 2xl (separation of sections)
64px  → 3xl (separation of major sections)
96px  → 4xl (page margins on desktop)
128px → 5xl (hero spacing)
```

### In CSS (custom properties)
```css
:root {
  --space-1: 4px;
  --space-2: 8px;
  --space-3: 12px;
  --space-4: 16px;
  --space-6: 24px;
  --space-8: 32px;
  --space-12: 48px;
  --space-16: 64px;
  --space-24: 96px;
  --space-32: 128px;
}
```

In Tailwind, this system corresponds to `p-1, p-2, p-3, p-4, p-6, p-8, p-12, p-16, p-24, p-32`.

---

## Spacing According to Logical Proximity

### Gestalt Principle: Proximity
Close elements are perceived as related. Spacing is the first tool for grouping.

**Rule:** Space between two unrelated elements must be **significantly larger** than between two related elements.

```
Section Title
  Paragraph related to title    ← small spacing between title and content
  
                                ← large spacing before next section
Next Section
```

### Ambiguous Spacing is a Mistake
If the space between A and B is identical to the space between B and C, the user doesn't know if B is related to A or C. Choose explicitly.

---

## White Space: Be Generous

Most interfaces lack space, not the other way around.

### Frequent Errors
- Buttons with insufficient padding (`padding: 4px 8px` for a primary button)
- Cards with content too tight against edges
- Sections with too little space between them
- Text in an input too close to the edge

### Practical Rule
If the interface looks "busy", try doubling spacing everywhere. Most of the time, it improves immediately.

---

## Spacing Does Not Scale Proportionally

### The Problem of Relative Scaling
If a `sm` button has `padding: 4px 8px` and a `lg` button has `padding: 12px 24px`, the `lg` button does not just have "3x the sm padding" — it has a **proportionally more generous** padding.

Large elements have a **relatively larger** padding than small ones, not just larger in absolute value.

```css
/* BAD: uniform proportional scaling */
.btn-sm { padding: 4px 8px; font-size: 12px; }   /* ratio 1:2 */
.btn-md { padding: 8px 16px; font-size: 16px; }  /* ratio 1:2 */
.btn-lg { padding: 12px 24px; font-size: 20px; } /* ratio 1:2 */

/* GOOD: relatively more generous padding on large */
.btn-sm { padding: 4px 10px; font-size: 12px; }
.btn-md { padding: 10px 20px; font-size: 16px; }
.btn-lg { padding: 16px 32px; font-size: 20px; } /* more generous in proportion */
```

---

## Grids

### 12-Column Grid as Base
Align the main layout on a 12-column grid. It offers enough flexibility (divides by 1, 2, 3, 4, 6, 12).

### Grids are Not Absolute Rules
Not all elements must be fluid and based on percentages:
- A sidebar can have a fixed width (240px, 280px)
- A modal has a fixed max-width
- An input has an ideal width according to expected content

**Do not outsource all layout decisions to the grid.**

---

## Grouping (Gestalt)

### Common Region: Containers Create Groups
Elements inside the same container (border, background, shadow) are perceived as belonging to the same group.

```
┌─────────────────────┐
│ Element A           │  ← A and B are perceived as related
│ Element B           │
└─────────────────────┘

  Element C              ← C is perceived as separate
```

### Types of Containers (from strongest to subtlest)
1. Different **Background color** → strong group
2. **Border** → strong group
3. **Shadow (box-shadow)** → strong group
4. **Proximity alone** → implicit group, less powerful

---

## Shadows and Depth

### Principle of Light Source
Light comes **from the top**. Simulate this in the interface:

- **Elevated elements** → lighter top edge + shadow under the element
- **Inset elements** → shadow at the top + lighter bottom edge

### Elevation System (5 levels)

```css
:root {
  /* Level 0: at surface level, no shadow */
  --shadow-none: none;

  /* Level 1: slightly elevated — buttons, badges */
  --shadow-sm:
    0 1px 2px hsla(220, 15%, 5%, 0.05),
    0 1px 1px hsla(220, 15%, 5%, 0.08);

  /* Level 2: cards, focused inputs */
  --shadow-md:
    0 2px 4px hsla(220, 15%, 5%, 0.06),
    0 4px 8px hsla(220, 15%, 5%, 0.08);

  /* Level 3: dropdowns, tooltips */
  --shadow-lg:
    0 4px 8px hsla(220, 15%, 5%, 0.08),
    0 8px 16px hsla(220, 15%, 5%, 0.12);

  /* Level 4: modals, popovers */
  --shadow-xl:
    0 8px 16px hsla(220, 15%, 5%, 0.10),
    0 16px 32px hsla(220, 15%, 5%, 0.16);
}
```

### Two-Shadow Technique
Combine a direct shadow (small, sharp, low blur) and an ambient shadow (large, soft, high blur):

```css
box-shadow:
  0 2px 4px rgba(0,0,0,0.12),     /* direct shadow: light */
  0 8px 24px rgba(0,0,0,0.08);    /* ambient shadow: diffuse */
```

Direct shadow becomes almost invisible at high elevation levels (the modal is so high that ambient light reaches it from everywhere).

### Shadows and Interaction
- `default` button → `--shadow-sm`
- `hover` button → `--shadow-md` (raises slightly)
- `active/pressed` button → `--shadow-none` or inset (sinks)
- `hover` card (draggable) → `--shadow-lg` (pop to front)

---

## Depth Without Shadows (Flat Design)

### Color as Depth
- Element lighter than background → perceived as elevated
- Element darker than background → perceived as inset

```css
/* Page background */
background: hsl(220, 14%, 97%);

/* Elevated card (lighter) */
.card { background: hsl(0, 0%, 100%); }

/* Inset well (darker) */
.well { background: hsl(220, 13%, 93%); }
```

### Solid Shadow (flat + depth)
```css
/* Shadow without blur — flat effect but with depth */
.card-flat {
  box-shadow: 4px 4px 0 hsl(220, 12%, 86%);
}
```

### Overlap
Overlap elements to create visual layers:
- A card that overlaps its parent container
- An avatar that overlaps two sections
- A badge that pops out of an image

---

## Images in Layout

### Control User Image Shapes
Never display images at their intrinsic ratio in a structured layout. Use fixed containers with `object-fit: cover`:

```css
.avatar {
  width: 48px;
  height: 48px;
  border-radius: 50%;
  object-fit: cover;
}
```

### Prevent Background Bleed
When an image has a background similar to the page background, use an internal shadow instead of a border:
```css
.user-image {
  box-shadow: inset 0 0 0 1px rgba(0,0,0,0.08);
}
```

### Icons: Respect Intentional Size
An icon designed for 16-24px will look "chunky" at 64px. If a large icon is needed, enclose it in a colored container and keep it at its native size.

```html
<div class="icon-container">  <!-- 64x64, colored background, rounded -->
  <svg class="icon">...</svg>   <!-- 20x20, native size -->
</div>
```