# 04 — Typographie

Sources : Refactoring UI ch.5 (Designing Text) · Practical UI ch.5 (Typography)

> **Note :** Ce fichier décrit les principes de choix typographique et les échelles standards. Pour générer une échelle typographique mathématique personnalisée (Type Scale ratio) ou gérer un rythme vertical (Baseline Grid), voir `math-typographie.md`. Pour rendre ces polices fluides, voir `responsive-math.md`.

---

## Système de tailles (type scale)

### Règle fondamentale
Ne jamais utiliser des tailles arbitraires. Définir une échelle fixe en amont et choisir uniquement dans cette échelle.

### Base : 16px
16px est la valeur par défaut des navigateurs. Elle se divise bien (÷2=8, ÷4=4) et sert de point de départ naturel.

### Échelle recommandée (en px / rem)
```
12px  / 0.75rem   → labels minuscules, captions
14px  / 0.875rem  → small text, helper text
16px  / 1rem      → corps de texte (base)
18px  / 1.125rem  → corps légèrement large
20px  / 1.25rem   → intro, lead paragraph
24px  / 1.5rem    → H4, sous-titres
30px  / 1.875rem  → H3
36px  / 2.25rem   → H2
48px  / 3rem      → H1 desktop
60px  / 3.75rem   → Hero title
72px  / 4.5rem    → Display
```

### Unités : px ou rem, jamais em
Les `em` sont relatifs à la taille de police de l'élément parent. Dans des éléments imbriqués, la taille calculée sort souvent de l'échelle définie.

```css
/* MAUVAIS - em imbriqués */
.parent { font-size: 1.25em; }  /* 20px */
.child  { font-size: 0.875em; } /* 17.5px — pas dans l'échelle ! */

/* BON - rem */
.parent { font-size: 1.25rem; } /* 20px */
.child  { font-size: 0.875rem; }/* 14px — dans l'échelle */
```

---

## Police de caractères

### Règle de base
- **1 police sans-serif** pour l'interface générale
- Optionnellement **1 police serif** pour les titres (émotion, personnalité)
- Maximum **2 familles** dans une même interface

### Choisir une bonne police sans-serif
Caractéristiques d'une bonne police UI :
- Hauteur d'x généreuse (lisibilité aux petites tailles)
- Formes ouvertes (le "c", le "g" ne se ferment pas trop)
- Chiffres tabulaires disponibles (pour les tables de données)

**Polices éprouvées :**
- Inter (libre, excellente aux petites tailles)
- SF Pro (Apple, natif macOS/iOS)
- Segoe UI (Microsoft, natif Windows)
- Roboto (Google, natif Android)

### Éviter
- Polices decoratives pour le corps de texte
- Polices condensées pour le texte de lecture
- Polices trop légères (thin) pour du texte fonctionnel

---

## Line-height (interligne)

### Règle : line-height proportionnel à la taille
Plus le texte est grand, plus le line-height doit être **petit**. L'espace absolu entre les lignes augmente de toute façon avec la taille de police.

| Contexte | Line-height recommandé |
|---|---|
| Corps de texte (16-18px) | 1.5 – 1.6 (150-160%) |
| Texte intermédiaire (20-24px) | 1.4 – 1.5 |
| Sous-titres (24-36px) | 1.3 – 1.4 |
| Titres (36px+) | 1.1 – 1.3 |
| Labels courts, une ligne | 1.0 – 1.2 |

---

## Longueur de ligne (line length)

### Zone idéale
**45 à 75 caractères** par ligne pour du texte de lecture.

En pratique, cela correspond à environ `60-75ch` en CSS :
```css
.prose {
  max-width: 65ch;
}
```

**Trop court** (< 45 char) : les sauts de ligne cassent le rythme de lecture.
**Trop long** (> 75 char) : difficile de retrouver le début de la ligne suivante.

---

## Alignement

### Règle générale : texte à gauche
Pour toutes les langues lues de gauche à droite, l'alignement gauche est la valeur par défaut pour le corps de texte.

### Centrer : uniquement pour les blocs courts indépendants
Centrer les titres courts, les CTA courts, les headlines — jamais des paragraphes.

```
✓ Centrer : un titre H1 isolé, un slogan, un label de section
✗ Centrer : plus de 2-3 lignes de texte consécutives
```

Si un bloc centré semble trop long, réécrire le contenu pour le raccourcir plutôt que changer l'alignement.

### Aligner les nombres à droite dans les tables
Les décimales restent ainsi alignées verticalement, facilitant la comparaison.

### Baseline alignment pour les tailles mixtes
Quand deux éléments de tailles différentes sont côte à côte, les aligner par la **baseline** (ligne de base des lettres), pas par le centre.

```css
.mixed-size-container {
  display: flex;
  align-items: baseline;  /* pas center */
}
```

---

## Letter-spacing

### Règle de base : faire confiance au designer de la police
Ne pas modifier le letter-spacing par défaut sauf dans deux cas :

**1. Titres en polices larges → réduire le letter-spacing**
Les polices conçues pour le corps de texte (larges espacements) semblent trop espacées en grande taille.
```css
h1 { letter-spacing: -0.025em; }
h2 { letter-spacing: -0.02em; }
```

**2. Texte en uppercase → augmenter le letter-spacing**
Les lettres majuscules ont toutes la même hauteur, ce qui les rend difficiles à lire sans espacement supplémentaire.
```css
.label-uppercase {
  text-transform: uppercase;
  letter-spacing: 0.05em;
  font-size: 12px;
  font-weight: 600;
}
```

---

## Poids de police (font-weight)

### Palette de poids recommandée pour l'UI
```
400 (Regular)  → corps de texte, valeurs de données
500 (Medium)   → labels, navigation
600 (Semibold) → sous-titres, éléments importants
700 (Bold)     → titres, données critiques
```

### Éviter
- `300` (Light) pour du texte fonctionnel — difficile à lire sur écran
- `900` (Black) sauf pour du display marketing

---

## Uppercase : usage restreint

### Quand utiliser uppercase
Uniquement pour des **labels courts** (2-4 mots maximum) :
- Catégories, sections
- Labels de méta-données
- Navigation secondaire

### Jamais uppercase pour
- Corps de texte
- Titres longs
- Boutons (sauf convention spécifique)
- Phrases entières

### Formatage correct pour l'uppercase
```css
.uppercase-label {
  text-transform: uppercase;
  letter-spacing: 0.06em;
  font-size: 11px;
  font-weight: 600;
  color: hsl(220, 10%, 55%);  /* secondaire, pas primaire */
}
```

---

## Liens : pas toujours en couleur

Dans un bloc de texte standard → les liens doivent se démarquer (couleur + underline).

Dans une interface où presque tout est un lien (navigation, dashboard) → utiliser des traitements plus subtils :
- Font-weight plus élevé
- Couleur légèrement plus foncée
- Underline visible uniquement au hover

Cela évite que l'interface entière soit envahie de bleu.