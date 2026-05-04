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

> **CRITICAL RULES FOR AI AGENTS:**
> 1. **Budget: Maximum 3 files per task.** Never load more than `core-principles` + 2 specific files.
> 2. **NEVER load all files.** Total framework = ~50,000 tokens. Loading everything wastes quota.
> 3. Always read `core-principles.md` FIRST. It covers 90% of design decisions.
> 4. Use the **Quick Routing** section below to pick the right 1-2 files per task.
> 5. **Cache rule:** Once you have read a file in this session, do NOT re-read it. Rely on context.
> 6. For concrete CSS values (colors, spacing, shadows), reference `tokens.md` — do NOT memorize values from other files.
> 7. **STRICT ISOLATION:** NEVER read files inside the `examples/` directory unless the user prompt explicitly includes keywords: "example", "template", "showcase", or "gold standard".

### Tier 1 — Always Available (~630 tokens)

Read on EVERY UI task. This is the only mandatory file.

| File | Content |
|------|---------|
| `references/core-principles.md` | **[READ FIRST]** The 10 golden rules for 90% of tasks |

### Tier 2 — Core References (load 1-2 via Quick Routing)

Load only the files indicated by Quick Routing for the specific user task.

| File | When to read it |
|------|-----------------|
| `references/composants.md` | Buttons, forms, tables, modals, states |
| `references/tokens.md` | Concrete values: colors, spacing, typography, shadows |
| `references/lois-ux.md` | UX psychology: Jakob, Fitts, Hick, Miller, etc. |
| `references/hierarchie-visuelle.md` | Visual hierarchy, weight, emphasis, buttons |
| `references/couleur-systeme.md` | Palette, contrast, HSL, color accessibility |
| `references/typographie.md` | Fonts, scale, line-height, alignment |
| `references/espacement-layout.md` | Spacing system, grids, shadows, depth |
| `references/processus-decisions.md` | Start a design, decide what to design first |
| `references/antipatterns-ethique.md` | Common mistakes, dark patterns, and fixes |
| `references/accessibilite-avancee.md` | ARIA, keyboard navigation, focus, reduced motion |

### Tier 3 — Specialized References (load ONLY when explicitly needed)

These files cover niche topics. Load only when the user specifically asks about the topic.

| File | When to read it |
|------|-----------------|
| `references/checklists-audit.md` | Quick audit before delivery |
| `references/checklists-composants.md` | Checklists for buttons, forms, modals |
| `references/checklists-layout.md` | Checklists for global view, flow, layout |
| `references/mode-sombre.md` | Dark mode design |
| `references/math-typographie.md` | Type scale ratios, golden ratio |
| `references/responsive-math.md` | clamp(), min(), max(), fluid grids |
| `references/couleur-math.md` | WCAG contrast ratios, OKLCH |
| `references/animations-math.md` | Cubic Bezier, springs, durations |
| `references/interactions-math.md` | Lerp, scroll velocity, requestAnimationFrame |
| `references/i18n-rtl.md` | Multi-language, RTL logical properties |
| `references/data-visualization.md` | Charts, accessible colors, dense tables |

### Tier 4 — Extensions (load ONLY when user explicitly asks)

Advanced patterns. **Never preload these.** Only load when the task matches.

| File | Trigger keywords |
|------|-----------------|
| `extensions/navigation-patterns.md` | "sidebar", "tabs", "breadcrumbs", "nav", "menu" |
| `extensions/ux-writing.md` | "button label", "error message", "empty state", "copy" |
| `extensions/performance-design.md` | "performance", "lighthouse", "CLS", "LCP", "speed" |
| `extensions/search-patterns.md" | "search", "filter", "autocomplete" |
| `extensions/icon-system.md` | "icon", "svg", "icon size" |
| `extensions/mobile-patterns.md` | "mobile", "touch", "bottom sheet", "gesture" |
| `extensions/media-guidelines.md` | "image", "avatar", "video", "aspect ratio", "alt text" |

### Tier 5 — Gold Standard Examples (LOAD ONLY ON DEMAND)

High-token files. **FORBIDDEN** for general design tasks. Load ONLY if user asks for examples.

| File | Purpose |
|------|---------|
| `examples/example-generate-dashboard.md` | Full dashboard implementation reference |
| `examples/example-generate-landing.md` | Full landing page implementation reference |
| `examples/example-review-form.md` | Detailed form review and correction reference |
| `examples/showcase-saas/` | Production-grade SaaS interface "Forma" |lt text" |

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
**"Build a navigation"** -> `navigation-patterns` + `lois-ux`
**"Write button labels/errors"** -> `ux-writing` + `antipatterns-ethique`
**"Optimize performance"** -> `performance-design` + `tokens`
**"Build a search interface"** -> `search-patterns` + `composants`
**"Choose/size icons"** -> `icon-system` + `accessibilite-avancee`
**"Design for mobile"** -> `mobile-patterns` + `responsive-math`
**"Handle images/avatars"** -> `media-guidelines` + `performance-design`
