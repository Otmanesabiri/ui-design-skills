# 11 — Mathématiques & Typographie

Source : Math for Web Design — Paul McFedries

---

## Type Scale : formule fondamentale

Chaque niveau d'une échelle typographique se calcule par :

```
Taille = Base × Ratio^n
```

- `Base` : taille de référence (16px recommandé)
- `Ratio` : le multiplicateur choisi
- `n` : l'échelon (positif = plus grand, négatif = plus petit)

### Exemple avec base 16px et ratio 1.25 (Major Third)

```
n = -2 → 16 × 1.25^-2 = 10.24px  → ~10px  (xs)
n = -1 → 16 × 1.25^-1 = 12.8px   → ~13px  (sm)
n =  0 → 16 × 1.25^0  = 16px     → 16px   (base)
n =  1 → 16 × 1.25^1  = 20px     → 20px   (lg)
n =  2 → 16 × 1.25^2  = 25px     → 25px   (xl)
n =  3 → 16 × 1.25^3  = 31.25px  → 31px   (2xl)
n =  4 → 16 × 1.25^4  = 39.06px  → 39px   (3xl)
n =  5 → 16 × 1.25^5  = 48.83px  → 49px   (4xl)
```

---

## Ratios disponibles et leurs usages

| Ratio | Nom | Valeur | Usage recommandé |
|-------|-----|--------|-----------------|
| Minor Second | Intervalle mineur | 1.067 | Interfaces très denses, peu de variation |
| Major Second | Ton entier | 1.125 | UI compactes, dashboards |
| Minor Third | Tierce mineure | 1.200 | **Interfaces UI standard** |
| Major Third | Tierce majeure | 1.250 | **Bon équilibre — recommandé** |
| Perfect Fourth | Quarte parfaite | 1.333 | Sites marketing, landing pages |
| Augmented Fourth | Triton | 1.414 | Titres expressifs |
| Perfect Fifth | Quinte parfaite | 1.500 | Affichage, grands écrans |
| Golden Ratio | Nombre d'Or | 1.618 | Très grand écart entre niveaux |

### Outil de calcul en JS

```javascript
function typeScale(base, ratio, steps) {
  return steps.map(n => ({
    step: n,
    size: +(base * Math.pow(ratio, n)).toFixed(2)
  }));
}

// Exemple : Major Third, base 16px, niveaux -2 à +5
const scale = typeScale(16, 1.25, [-2, -1, 0, 1, 2, 3, 4, 5]);
```

---

## Nombre d'Or (Golden Ratio — 1.618)

### En typographie

Le ratio 1.618 entre deux tailles crée une relation visuelle naturellement harmonieuse.

```css
/* Corps de texte → Titre H1 */
--text-base: 16px;
--text-h1: calc(16px * 1.618 * 1.618); /* ~41.9px */

/* Ou appliqué progressivement */
--text-base: 1rem;     /* 16px */
--text-lg: 1.618rem;   /* 25.9px */
--text-xl: 2.618rem;   /* 41.9px */
```

### En layout

```css
/* Sidebar / Contenu principal */
.layout {
  display: grid;
  grid-template-columns: 1fr 1.618fr;
  /* Sidebar ≈ 38% | Contenu ≈ 62% */
}

/* Equivalent en 12 colonnes : sidebar 4-5 col, contenu 7-8 col */
```

---

## Line-height : les deux règles mathématiques

### Règle 1 : inversement proportionnel à la taille
Plus la police est grande, moins il faut d'interligne supplémentaire.

```
line-height ↓ quand font-size ↑
```

| Taille | Line-height recommandé |
|--------|----------------------|
| 12-14px | 1.6 – 1.8 |
| 16-18px | 1.5 – 1.6 |
| 20-24px | 1.4 – 1.5 |
| 30-36px | 1.2 – 1.35 |
| 48px+   | 1.0 – 1.2 |

### Règle 2 : proportionnel à la longueur de ligne
Plus la colonne est large, plus le line-height doit être élevé pour aider l'œil au retour à la ligne.

```
line-height ↑ quand line-length ↑
```

| Largeur de colonne | Line-height recommandé |
|--------------------|----------------------|
| < 45 caractères | 1.3 – 1.4 |
| 45-65 caractères | 1.5 – 1.6 |
| 65-80 caractères | 1.6 – 1.75 |
| > 80 caractères | 1.75 – 2.0 |

---

## Rythme vertical (Baseline Grid)

### Principe
Tous les éléments de la page s'alignent sur une grille de lignes imaginaires espacées d'une valeur fixe. Cela crée un rythme visuel cohérent.

### Calcul

```
Baseline unit = line-height en px du corps de texte

Exemple : 16px × 1.5 = 24px → baseline unit = 24px
```

Tous les espacements verticaux (margin, padding, gap) sont des multiples de cette valeur :
```css
:root {
  --baseline: 24px;  /* 16px × 1.5 */

  --space-half:  calc(var(--baseline) * 0.5);  /* 12px */
  --space-1:     var(--baseline);               /* 24px */
  --space-2:     calc(var(--baseline) * 2);     /* 48px */
  --space-3:     calc(var(--baseline) * 3);     /* 72px */
  --space-4:     calc(var(--baseline) * 4);     /* 96px */
}
```

### Alignement baseline dans le code

```css
/* Aligner par baseline, pas par centre */
.mixed-sizes {
  display: flex;
  align-items: baseline;  /* jamais "center" pour du texte mixte */
}
```
