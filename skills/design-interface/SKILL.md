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
| `references/01-processus.md` | Démarrer un design, décider quoi designer en premier |
| `references/02-hierarchie.md` | Hiérarchie visuelle, poids, emphasis, boutons |
| `references/03-couleur.md` | Palette, contraste, HSL, accessibilité couleur |
| `references/04-typographie.md` | Polices, échelle, line-height, alignement |
| `references/05-espacement-layout.md` | Spacing system, grilles, ombres, profondeur |
| `references/06-lois-ux.md` | Psychologie UX, Jakob, Fitts, Hick, Miller, etc. |
| `references/07-composants.md` | Boutons, formulaires, tables, modales, états |
| `references/08-tokens.md` | Valeurs concrètes : couleurs, espacement, typographie, ombres |
| `references/09-antipatterns.md` | Erreurs fréquentes et corrections |
| `references/10-checklists.md` | Checklists de review complètes par catégorie |

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

**"Review ce composant"** → `02-hierarchie` + `07-composants` + `10-checklists`
**"Crée une palette"** → `03-couleur` + `08-tokens`
**"Design ce formulaire"** → `07-composants` + `05-espacement-layout`
**"Quel shadow utiliser ?"** → `05-espacement-layout` + `08-tokens`
**"Pourquoi ce design ne fonctionne pas ?"** → `02-hierarchie` + `09-antipatterns`
**"Accessibilité de l'interface"** → `03-couleur` + `10-checklists`
**"Justifier une décision design"** → `06-lois-ux`