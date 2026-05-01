# 12 — CSS Fluide & Responsive Math

Source : Math for Web Design — Paul McFedries

---

## `clamp()` : la formule fondamentale

```css
clamp(MIN, PREFERRED, MAX)
```

Équivalent mathématique : `max(MIN, min(PREFERRED, MAX))`

Le navigateur retourne :
- `MIN` si `PREFERRED < MIN`
- `PREFERRED` si `MIN ≤ PREFERRED ≤ MAX`
- `MAX` si `PREFERRED > MAX`

---

## Calcul de la valeur `preferred` fluide

Pour qu'une valeur soit **exactement proportionnelle** entre deux breakpoints :

### Formule

```
slope = (maxValue - minValue) / (maxVW - minVW)
preferred = slope × 100vw + intercept
intercept = minValue - slope × minVW
```

### Exemple concret : font-size fluide de 16px à 24px entre 320px et 1280px

```
slope = (24 - 16) / (1280 - 320) = 8 / 960 = 0.00833
preferred = 0.00833 × 100vw = 0.833vw
intercept = 16 - 0.00833 × 320 = 16 - 2.67 = 13.33px

→ clamp(16px, 13.33px + 0.833vw, 24px)
```

En CSS :
```css
font-size: clamp(1rem, 0.833rem + 0.833vw, 1.5rem);
```

### Outil de calcul JS

```javascript
function fluidValue(minVal, maxVal, minVW, maxVW) {
  const slope = (maxVal - minVal) / (maxVW - minVW);
  const intercept = minVal - slope * minVW;
  return {
    clamp: `clamp(${minVal}px, ${intercept.toFixed(4)}px + ${(slope * 100).toFixed(4)}vw, ${maxVal}px)`,
    slope,
    intercept
  };
}

// Usage
fluidValue(16, 24, 320, 1280);
// → clamp(16px, 13.3333px + 0.8333vw, 24px)
```

---

## Type scale fluide complète

```css
:root {
  /* xs : 12px → 14px */
  --text-xs: clamp(0.75rem, 0.7083rem + 0.2083vw, 0.875rem);

  /* sm : 14px → 16px */
  --text-sm: clamp(0.875rem, 0.8333rem + 0.2083vw, 1rem);

  /* base : 16px → 18px */
  --text-base: clamp(1rem, 0.9583rem + 0.2083vw, 1.125rem);

  /* lg : 18px → 22px */
  --text-lg: clamp(1.125rem, 1.0417rem + 0.4167vw, 1.375rem);

  /* xl : 20px → 26px */
  --text-xl: clamp(1.25rem, 1.125rem + 0.625vw, 1.625rem);

  /* 2xl : 24px → 36px */
  --text-2xl: clamp(1.5rem, 1.25rem + 1.25vw, 2.25rem);

  /* 3xl : 30px → 48px */
  --text-3xl: clamp(1.875rem, 1.5rem + 1.875vw, 3rem);

  /* 4xl : 36px → 64px */
  --text-4xl: clamp(2.25rem, 1.6667rem + 2.9167vw, 4rem);

  /* 5xl : 48px → 80px */
  --text-5xl: clamp(3rem, 2.3333rem + 3.3333vw, 5rem);
}
```

---

## Spacing tokens fluides

```css
:root {
  /* espace-1 : 4px → 8px */
  --space-1: clamp(0.25rem, 0.1667rem + 0.4167vw, 0.5rem);

  /* espace-2 : 8px → 12px */
  --space-2: clamp(0.5rem, 0.4167rem + 0.4167vw, 0.75rem);

  /* espace-4 : 16px → 24px */
  --space-4: clamp(1rem, 0.8333rem + 0.8333vw, 1.5rem);

  /* espace-6 : 24px → 40px */
  --space-6: clamp(1.5rem, 1.1667rem + 1.6667vw, 2.5rem);

  /* espace-8 : 32px → 64px */
  --space-8: clamp(2rem, 1.3333rem + 3.3333vw, 4rem);

  /* espace-12 : 48px → 96px */
  --space-12: clamp(3rem, 2rem + 5vw, 6rem);

  /* espace-16 : 64px → 128px */
  --space-16: clamp(4rem, 2.6667rem + 6.6667vw, 8rem);
}
```

---

## `min()` et `max()` : cas d'usage

### `min()` — valeur la plus petite
```css
/* Largeur ne dépassant jamais 600px mais pouvant être plus petite */
.container {
  width: min(600px, 100%);
}

/* Padding qui ne dépasse pas 5% de la largeur */
.section {
  padding-inline: min(5%, 48px);
}
```

### `max()` — valeur la plus grande
```css
/* Font-size jamais en dessous de 16px */
p {
  font-size: max(16px, 1.5vw);
}

/* Hauteur minimale garantie */
.hero {
  min-height: max(400px, 50vh);
}
```

---

## Grilles proportionnelles sans breakpoints

### Formule de la grille auto-adaptative

```css
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(MIN, 1fr));
}
```

Le navigateur calcule le nombre de colonnes :
```
n = floor((largeurConteneur - sommeGaps) / MIN)
```

### Exemples concrets

```css
/* Grille de cards : 3 colonnes sur desktop, 1 sur mobile */
.cards-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: var(--space-6);
}

/* Grille de tags : s'adapte au contenu */
.tags-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(120px, 1fr));
  gap: var(--space-2);
}
```

### Grille Golden Ratio

```css
/* Sidebar + Contenu (ratio 1:1.618) */
.golden-layout {
  display: grid;
  grid-template-columns: 1fr 1.618fr;
  gap: var(--space-8);
}

/* Responsive : stack sur mobile */
@media (max-width: 768px) {
  .golden-layout {
    grid-template-columns: 1fr;
  }
}
```

### Grille de colonnes `fr` : calcul

Pour `grid-template-columns: 1fr 2fr 1fr` avec un conteneur de 960px et 2 gaps de 24px :

```
Espace restant = 960 - (2 × 24) = 912px
Total fr = 1 + 2 + 1 = 4fr
1fr = 912 / 4 = 228px
2fr = 456px
```

---

## `calc()` : algèbre en CSS

### Cas d'usage

```css
/* Largeur = 100% moins une sidebar fixe */
.main-content {
  width: calc(100% - 280px);
}

/* Padding qui prend en compte la scrollbar */
.modal {
  padding-right: calc(var(--space-8) + var(--scrollbar-width, 0px));
}

/* Font-size intermédiaire entre deux valeurs système */
.special-text {
  font-size: calc((var(--text-lg) + var(--text-xl)) / 2);
}

/* Hauteur fullscreen moins le header */
.hero {
  min-height: calc(100vh - 64px);
  min-height: calc(100dvh - 64px); /* dynamic viewport height */
}
```

### Précautions

```css
/* ✓ Bon : unités compatibles dans l'opération */
width: calc(100% - 48px);

/* ✗ Mauvais : division par une valeur avec unité */
font-size: calc(32px / 2px);  /* invalide */
font-size: calc(32px / 2);    /* valide → 16px */
```

---

## Pourcentages verticaux : le piège

En CSS, les `margin` et `padding` en pourcentage (même `margin-top`, `padding-bottom`) sont calculés par rapport à la **largeur du parent**, pas la hauteur.

```css
/* padding-top: 56.25% = ratio 16:9 (100/16×9) */
.video-wrapper {
  position: relative;
  width: 100%;
  padding-top: 56.25%; /* 9/16 = 0.5625 */
}

.video-wrapper > iframe {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
}
```

Cela permet de maintenir des ratios d'aspect constants quelle que soit la largeur du conteneur.
