# 02 — Visual Hierarchy

Sources: Refactoring UI ch.2 · Practical UI ch.4 (Layout) · Laws of UX ch.8 (Von Restorff)

---

## Fundamental Principle

> "When everything in an interface is competing for attention, it feels loud and chaotic — like a letter where every word is underlined."

Visual hierarchy is **the most impactful factor** in perceiving a design as "successful". It precedes all other aesthetic criteria.

**De-emphasizing secondary elements is as important as emphasizing primary ones.**

---

## Hierarchy Levers

Do not use size alone. Combine several levers:

| Lever | Usage | Example |
|--------|-------|---------|
| **Size** | Differentiate major levels | H1 title vs body |
| **Weight (font-weight)** | Emphasize without changing size | `font-weight: 700` on an important label |
| **Color / Contrast** | Differentiate primary, secondary, tertiary | Black for main, dark gray for secondary, light gray for tertiary |
| **Spacing** | Group and separate | More space between unrelated sections |
| **Opacity** | Soften without changing color | `opacity: 0.5` on helper text |

### Color Scale for Text Hierarchy
```
Primary text    → hsl(220, 15%, 10%)   // quasi-black
Secondary text  → hsl(220, 10%, 40%)   // dark-medium gray
Tertiary text   → hsl(220, 8%, 60%)    // medium gray
Disabled text   → hsl(220, 5%, 75%)    // light gray
```

---

## Action Hierarchy (Buttons)

Every action on a page occupies a position in an importance pyramid.

### The Three Levels
```
Primary   → Solid, strong color, immediately visible
Secondary → Outline or low contrast background, clear but not prominent
Tertiary  → Link style, discreet but discoverable
```

### Critical Rule
**Semantics are secondary to hierarchy.**

A "Delete" button (danger) can very well be tertiary if it is not the main action of the page. The "danger = red" style does not imply "danger = primary button".

**Bad:**
```
[Save]  [Delete]  ← two buttons with the same visual weight
```

**Good:**
```
[Save]  Delete   ← delete is a link, not a button
```

### Maximum 1 Primary Button Per Section
If two buttons seem equally important, review the action hierarchy — one of the two is necessarily more important.

---

## Data Hierarchy (Labels)

### Problem with the `Label: Value` format
This format gives the same weight to each piece of data. It makes it difficult to create hierarchy in a set of data.

### Alternatives in Order of Preference

**1. No label at all**
If the data format is self-explanatory:
```
janedoe@example.com   ✓ (no need for "Email:")
(555) 765-4321         ✓ (no need for "Phone:")
$19.99                 ✓ (no need for "Price:")
```

**2. Label integrated into the value**
```
12 in stock            ✓ (rather than "Stock: 12")
Member since 2019     ✓ (rather than "Member since: 2019")
```

**3. Discreet support label**
If the label is necessary, make it visually secondary:
```css
.label {
  font-size: 12px;
  font-weight: 500;
  color: hsl(220, 10%, 55%);
  text-transform: uppercase;
  letter-spacing: 0.05em;
}
.value {
  font-size: 16px;
  font-weight: 600;
  color: hsl(220, 15%, 10%);
}
```

**4. Label: Value** — only as a last resort

---

## The Squint Test (Practical UI)

To test an interface's hierarchy: **squint your eyes until everything is blurry**.

What remains visible = correctly prioritized elements.
What disappears into the noise = too weak elements.
What stands out too much = too strong elements.

If everything disappears at the same rate, hierarchy is absent.

---

## Von Restorff Effect (Laws of UX)

> "Among similar objects, the one that differs is most remembered."

### Application
- The most important element of a page must differ visually from its neighbors
- A badge, an accent color, a different size — any visual break attracts attention

### Caution
**Do not over-use this effect.** If everything is highlighted, nothing is. Reserve differentiation for 1 or 2 elements maximum per view.

---

## Hierarchy in Multi-Step Forms

Recommended Structure:
```
Step title      → H2, strong weight, primary color
Subtitle/context → body, secondary color
Field labels    → uppercase small, tertiary color
Field values    → body, primary color
Actions         → single primary button on the right
Back link       → tertiary link on the left
```

---

## Depth as a Hierarchy Lever (Practical UI)

Depth (shadows, layering) creates a spatial hierarchy:
- Foreground elements (modals, dropdowns) → strong shadows
- Page-level elements (cards) → light shadows
- In-page elements (section background) → no shadow, background color difference

```css
/* Elevation levels */
--shadow-sm: 0 1px 2px hsla(220, 15%, 10%, 0.08);         /* buttons */
--shadow-md: 0 4px 8px hsla(220, 15%, 10%, 0.12);         /* cards */
--shadow-lg: 0 8px 24px hsla(220, 15%, 10%, 0.16);        /* dropdowns */
--shadow-xl: 0 16px 48px hsla(220, 15%, 10%, 0.20);       /* modals */
```