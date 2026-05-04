# Icon System

Sources: Material Design · Lucide Icons · Apple HIG · WCAG 2.2

> **Agent Instruction:** Load this file ONLY when choosing, sizing, or implementing icons. For ARIA rules on icons, see `references/accessibilite-avancee.md`. For CSS values, reference `references/tokens.md`.

---

## Icon Sizing Scale

| Size | px | Usage |
|------|-----|-------|
| **xs** | 12px | Inline text indicators (chevrons, sort arrows) |
| **sm** | 16px | Inside buttons, input prefixes, table actions |
| **md** | 20px | Navigation links, form field icons |
| **lg** | 24px | Sidebar navigation, card headers |
| **xl** | 32px | Feature cards, empty states |
| **2xl** | 48px | Hero illustrations, onboarding |

```css
:root {
  --icon-xs:  12px;
  --icon-sm:  16px;
  --icon-md:  20px;
  --icon-lg:  24px;
  --icon-xl:  32px;
  --icon-2xl: 48px;
}

svg, .icon {
  flex-shrink: 0; /* never let icons shrink in flex layouts */
}
```

---

## Style Consistency

### Rule: One style per project

| Style | Best For | Example Libraries |
|-------|----------|-------------------|
| **Outline (stroke)** | SaaS, dashboards, professional tools | Lucide, Heroicons Outline |
| **Filled (solid)** | Mobile apps, active states, emphasis | Heroicons Solid, Material Filled |
| **Duotone** | Marketing pages, illustrations | Phosphor Duotone |

```
❌ Never mix outline and filled icons in the same section
✅ Exception: use filled version for "active" state in navigation

Sidebar example:
  ○ Dashboard (outline = inactive)
  ● Dashboard (filled = active)
```

### Stroke Width Consistency

```css
/* All SVG icons must share the same stroke-width */
svg {
  stroke-width: 1.5; /* or 2 — pick one, stay consistent */
  stroke-linecap: round;
  stroke-linejoin: round;
  fill: none;
}
```

---

## Icon + Text Rules

### When to use icon alone vs icon + text

| Context | Recommendation |
|---------|---------------|
| Navigation sidebar | Icon + Text always |
| Collapsed sidebar | Icon only + tooltip |
| Toolbar with > 5 actions | Icon only + tooltip |
| Primary button | Text only (or icon + text, never icon alone) |
| Table row action | Icon only if universally understood (edit ✏️, delete 🗑️) |
| Mobile bottom nav | Icon + short label always |

### Spacing Between Icon and Text

```css
/* Button with icon */
.btn-with-icon {
  display: inline-flex;
  align-items: center;
  gap: 6px; /* --space-1-5: tight coupling */
}

/* Navigation link */
.nav-link {
  display: flex;
  align-items: center;
  gap: 10px; /* --space-2-5: comfortable reading */
}

/* Feature card heading */
.feature-icon + .feature-title {
  margin-top: 12px; /* --space-3: visual separation */
}
```

---

## Accessibility Rules

### Decorative Icons (accompanies text)

```html
<!-- Icon is redundant — text already conveys meaning -->
<button>
  <svg aria-hidden="true" focusable="false"><!-- save icon --></svg>
  Save changes
</button>
```

### Standalone Icons (no text)

```html
<!-- Icon is the ONLY indication — must have label -->
<button aria-label="Delete merchant">
  <svg aria-hidden="true" focusable="false"><!-- trash icon --></svg>
</button>

<!-- Alternative: use title + sr-only text -->
<button>
  <svg aria-hidden="true"><!-- close icon --></svg>
  <span class="sr-only">Close dialog</span>
</button>
```

### Status Icons (convey meaning)

```html
<!-- Icon represents a status — needs role="img" + aria-label -->
<span role="img" aria-label="Transaction successful">
  <svg aria-hidden="true"><!-- checkmark --></svg>
</span>

<!-- NEVER rely on color alone — icon shape must differ -->
✅ Success: ✓ (checkmark, green)
✅ Error:   ✗ (cross, red)
✅ Warning: ⚠ (triangle, amber)
✅ Info:    ℹ (circle-i, blue)
```

---

## Icon Color Rules

```css
/* Icons inherit text color by default */
svg {
  color: currentColor;
  stroke: currentColor;
}

/* Semantic icon colors (match your token system) */
.icon-success { color: var(--success-600); }
.icon-error   { color: var(--error-600); }
.icon-warning { color: var(--warning-600); }
.icon-info    { color: var(--info-600); }
.icon-muted   { color: var(--color-text-tertiary); }

/* Interactive icons: show state change */
.icon-btn {
  color: var(--color-text-secondary);
  transition: color var(--duration-base) var(--ease-out);
}
.icon-btn:hover { color: var(--color-text-primary); }
.icon-btn:active { color: var(--color-brand); }
```

---

## Implementation: SVG Inline vs Sprite vs Font

| Method | Pros | Cons | Use When |
|--------|------|------|----------|
| **Inline SVG** | Full CSS control, no HTTP request | Bloats HTML | < 20 icons per page |
| **SVG Sprite** | Single request, cacheable | Setup required | 20+ icons, multi-page app |
| **Icon Font** | Simple CSS | Blurry on some screens, accessibility issues | ❌ Avoid |
| **Component** | Framework integration (Vue/React) | Build step | Nuxt/Next projects |

### Nuxt/Vue Component Pattern

```vue
<!-- components/Icon.vue -->
<template>
  <svg
    :width="size"
    :height="size"
    viewBox="0 0 24 24"
    fill="none"
    stroke="currentColor"
    :stroke-width="strokeWidth"
    stroke-linecap="round"
    stroke-linejoin="round"
    aria-hidden="true"
    focusable="false"
  >
    <slot />
  </svg>
</template>

<script setup>
defineProps({
  size: { type: [Number, String], default: 20 },
  strokeWidth: { type: [Number, String], default: 1.5 }
})
</script>
```

---

## Checklist

```
Consistency
[ ] Single icon style used (outline OR filled, not mixed)
[ ] Consistent stroke-width across all icons
[ ] Icon sizes follow the scale (12/16/20/24/32/48)

Accessibility
[ ] Decorative icons have aria-hidden="true"
[ ] Standalone icons have aria-label
[ ] Status icons use shape + color (not color alone)

Usage
[ ] Icon + text in navigation (never icon-only without tooltip)
[ ] Primary buttons use text (icon optional, never icon-only)
[ ] Mobile bottom nav always has icon + label

Performance
[ ] Inline SVG for < 20 icons, sprite for 20+
[ ] No icon fonts used
[ ] Icons are properly sized (no 24px icon scaled to 12px)
```
