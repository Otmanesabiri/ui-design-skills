---
name: ui-design-interface
description: Génère, améliore et relit des interfaces utilisateur. Use when the user wants to review, improve, or generate UI layouts or components.
---

# UI Design Interface

Quick start
- Demandez "/generate-ui" pour générer une interface.
- Demandez "/improve-ui" pour améliorer une maquette.
- Demandez "/review-ui" pour obtenir un feedback structuré.
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

# UI Design Skill — Index

Sources : **Refactoring UI** · **Laws of UX (2e éd.)** · **Practical UI**

---

## Architecture des fichiers

Lis le(s) fichier(s) de référence correspondant à la tâche demandée.
Ne charge pas tout — lis uniquement ce dont tu as besoin.

| Fichier | Quand le lire |
|---------|--------------|
| `references/processus-decisions.md` | Démarrer un design, décider quoi designer en premier |
| `references/hierarchie-visuelle.md` | Hiérarchie visuelle, poids, emphasis, boutons |
| `references/couleur-systeme.md` | Palette, contraste, HSL, accessibilité couleur |
| `references/typographie.md` | Polices, échelle, line-height, alignement |
| `references/espacement-layout.md` | Spacing system, grilles, ombres, profondeur |
| `references/lois-ux.md` | Psychologie UX, Jakob, Fitts, Hick, Miller, etc. |
| `references/composants.md` | Boutons, formulaires, tables, modales, états |
| `references/tokens.md` | Valeurs concrètes : couleurs, espacement, typographie, ombres |
| `references/antipatterns-ethique.md` | Erreurs fréquentes, Dark patterns et corrections |
| `references/checklists.md` | Checklists de review complètes par catégorie |
| `references/mode-sombre.md` | Inversion HSL, palette sombre, design de Dark Mode |
| `references/math-typographie.md` | Type scale par ratio, Golden Ratio, baseline grid |
| `references/responsive-math.md` | clamp(), min(), max(), calc(), grilles fluides |
| `references/couleur-math.md` | Contrast ratio WCAG, palette HSL, OKLCH, dark mode |
| `references/animations-math.md` | Cubic Bezier, spring, trigonométrie, durées |
| `references/interactions-math.md` | Lerp, mapping, scroll vélocité, requestAnimationFrame |

---

## Règles non-négociables

1. **Partir d'une feature, pas d'un layout** — ne jamais commencer par la nav ou le shell
2. **Hiérarchie avant esthétique** — si la hiérarchie est cassée, la couleur ne sauvera rien
3. **Contraste WCAG AA minimum** — 4.5:1 texte normal, 3:1 grand texte et composants UI
4. **Système, pas valeurs arbitraires** — espacement, couleur, typo depuis des échelles fixes
5. **La couleur ne peut pas être le seul indicateur** — toujours doubler avec icône ou texte
6. **1 bouton primaire par section** — pas deux actions de même poids en compétition
7. **Concevoir en noir et blanc d'abord** — ajouter la couleur en dernier
8. **Tout détail a une raison logique** — pas de décoration sans justification fonctionnelle

---

## Routing rapide

**"Review ce composant"** → `hierarchie-visuelle` + `composants` + `checklists`
**"Crée une palette"** → `couleur-systeme` + `tokens`
**"Design ce formulaire"** → `composants` + `espacement-layout`
**"Quel shadow utiliser ?"** → `espacement-layout` + `tokens`
**"Pourquoi ce design ne fonctionne pas ?"** → `hierarchie-visuelle` + `antipatterns-ethique`
**"Accessibilité de l'interface"** → `couleur-systeme` + `checklists`
**"Justifier une décision design"** → `lois-ux`
**"Ajouter le mode sombre"** → `mode-sombre` + `couleur-systeme`
**"Type scale harmonieuse"** → `math-typographie` + `typographie`
**"Typographie / spacing fluide"** → `responsive-math` + `tokens`
**"Contrast ratio exact"** → `couleur-math` + `couleur-systeme`
**"Animer un composant"** → `animations-math`
**"Effet scroll / parallax / cursor"** → `interactions-math`