---
name: ui-design-interface
description: Generates, improves, and reviews user interfaces. Use when the user wants to review, improve, or generate UI layouts or components.
---

# UI Design Interface

Quick start
- Ask "/generate-ui" to generate an interface.
- Ask "/improve-ui" to improve a mockup.
- Ask "/review-ui" to get structured feedback.

---
name: ui-design-skill
description: >
  Use this skill whenever designing, reviewing, refactoring, or critiquing any UI component,
  screen, or interface. Triggers include: designing from scratch, reviewing for visual issues,
  choosing colors/typography/spacing, evaluating hierarchy, building forms/buttons/modals/tables,
  asking "does this look good?", "how do I improve this?", "what's wrong with this design?",
  "how should I design X?", or any UI/UX decision. Based on Refactoring UI (Wathan & Schoger),
  Laws of UX 2nd ed. (Yablonski), and Practical UI (Dannaway). Always use this skill before
  generating or reviewing any interface code or design.
---

# UI Design Skill - Index

Sources: **Refactoring UI** - **Laws of UX (2nd ed.)** - **Practical UI**

---

## File Architecture (Token Optimization)

> **CRITICAL RULE FOR AI AGENTS:** 
> 1. Always read `core-principles.md` first. It contains 90% of what you need.
> 2. Rely on your context caching: once you know a principle, do not re-read the file.
> 3. ONLY load other specific files if the user asks for exact tokens, mathematical formulas, or deep component reviews.

| File | When to read it |
|------|------------------|
| `references/core-principles.md` | **[READ FIRST]** The 10 golden rules for 90% of tasks |
| `references/processus-decisions.md` | Start a design, decide what to design first |
| `references/hierarchie-visuelle.md` | Visual hierarchy, weight, emphasis, buttons |
| `references/couleur-systeme.md` | Palette, contrast, HSL, color accessibility |
| `references/typographie.md` | Fonts, scale, line-height, alignment |
| `references/espacement-layout.md` | Spacing system, grids, shadows, depth |
| `references/lois-ux.md` | UX psychology: Jakob, Fitts, Hick, Miller, etc. |
| `references/composants.md` | Buttons, forms, tables, modals, states |
| `references/tokens.md` | Concrete values: colors, spacing, typography, shadows |
| `references/antipatterns-ethique.md` | Common mistakes, dark patterns, and fixes |
| `references/checklists-audit.md` | Quick audit before delivery, Red flags |
| `references/checklists-composants.md` | Checklists for buttons, forms, modals, states |
| `references/checklists-layout.md` | Checklists for global view, flow, and layout |
| `references/mode-sombre.md` | HSL inversion, dark palette, dark mode design |
| `references/math-typographie.md` | Type scale ratios, golden ratio, baseline grid |
| `references/responsive-math.md` | clamp(), min(), max(), calc(), fluid grids |
| `references/couleur-math.md` | Exact WCAG contrast ratios, HSL palette, OKLCH, dark mode |
| `references/animations-math.md` | Cubic Bezier, springs, trigonometry, durations |
| `references/interactions-math.md` | Lerp, mapping, scroll velocity, requestAnimationFrame |
| `references/accessibilite-avancee.md` | ARIA, keyboard navigation, focus, reduced motion |
| `references/i18n-rtl.md` | Multi-language, RTL logical properties, text expansion |
| `references/data-visualization.md` | Charts, accessible colors, dense data tables |

---

## Non-Negotiable Rules

1. **Start from a feature, not a layout** -- never start with nav or shell
2. **Hierarchy before aesthetics** -- if hierarchy is broken, color won't save it
3. **WCAG AA minimum contrast** -- 4.5:1 normal text, 3:1 large text and UI components
4. **System, not arbitrary values** -- spacing/color/type from fixed scales
5. **Color can't be the only signal** -- always back it up with an icon or text
6. **One primary button per section** -- don't make two equally-weighted actions compete
7. **Design in black & white first** -- add color last
8. **Every detail has a logical reason** -- no decoration without functional justification

---

## Quick Routing

**"Review this component"** -> `hierarchie-visuelle` + `checklists-composants`
**"General audit"** -> `checklists-audit` + `core-principles`
**"Create a palette"** -> `couleur-systeme` + `tokens`
**"Design this form"** -> `composants` + `espacement-layout`
**"Which shadow should I use?"** -> `espacement-layout` + `tokens`
**"Why doesn't this design work?"** -> `hierarchie-visuelle` + `antipatterns-ethique`
**"Interface accessibility"** -> `couleur-systeme` + `checklists-audit`
**"Justify a design decision"** -> `lois-ux`
**"Add dark mode"** -> `mode-sombre` + `couleur-systeme`
**"Harmonious type scale"** -> `math-typographie` + `typographie`
**"Fluid typography/spacing"** -> `responsive-math` + `tokens`
**"Exact contrast ratio"** -> `couleur-math` + `couleur-systeme`
**"Animate a component"** -> `animations-math`
**"Scroll/parallax/cursor effect"** -> `interactions-math`
**"Advanced accessibility / ARIA"** -> `accessibilite-avancee` + `core-principles`
**"RTL or multi-language design"** -> `i18n-rtl`
**"Design a chart or data table"** -> `data-visualization` + `couleur-systeme`
