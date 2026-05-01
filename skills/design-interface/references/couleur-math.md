# 13 — Mathématiques & Couleur

Source : Math for Web Design — Paul McFedries

---

## Calcul du contrast ratio (WCAG)

### Formule officielle

```
CR = (L1 + 0.05) / (L2 + 0.05)
```

- `L1` : luminance relative de la couleur la plus **claire**
- `L2` : luminance relative de la couleur la plus **sombre**
- `CR` : contrast ratio (1:1 = aucun contraste, 21:1 = noir sur blanc)

### Calcul de la luminance relative

```javascript
function getLuminance(r, g, b) {
  // Normaliser 0-255 → 0-1
  const [rs, gs, bs] = [r, g, b].map(c => {
    c = c / 255;
    return c <= 0.03928
      ? c / 12.92
      : Math.pow((c + 0.055) / 1.055, 2.4);
  });
  // Formule WCAG
  return 0.2126 * rs + 0.7152 * gs + 0.0722 * bs;
}

function contrastRatio(color1RGB, color2RGB) {
  const L1 = getLuminance(...color1RGB);
  const L2 = getLuminance(...color2RGB);
  const lighter = Math.max(L1, L2);
  const darker  = Math.min(L1, L2);
  return +((lighter + 0.05) / (darker + 0.05)).toFixed(2);
}

// Exemple
contrastRatio([255, 255, 255], [0, 0, 0]);     // → 21
contrastRatio([255, 255, 255], [100, 100, 100]); // → 5.9 (AA ✓)
```

### Seuils WCAG 2.1

| Niveau | Texte normal | Grand texte (≥18px ou bold ≥14px) | UI Components |
|--------|-------------|-----------------------------------|---------------|
| AA     | **4.5:1**   | **3:1**                           | **3:1**       |
| AAA    | 7:1         | 4.5:1                             | N/A           |

---

## Génération de palette HSL : algorithme

### Méthode des 3 ancres + interpolation

```javascript
function generatePalette(hue, saturation) {
  // 3 ancres : très clair (100), base (500), très foncé (900)
  const anchors = {
    100: { s: saturation * 0.4, l: 94 },
    500: { s: saturation,       l: 50 },
    900: { s: saturation * 0.6, l: 15 }
  };

  // Interpolation linéaire entre ancres
  function interpolate(step) {
    if (step <= 500) {
      const t = (step - 100) / 400;
      return {
        s: anchors[100].s + (anchors[500].s - anchors[100].s) * t,
        l: anchors[100].l + (anchors[500].l - anchors[100].l) * t
      };
    } else {
      const t = (step - 500) / 400;
      return {
        s: anchors[500].s + (anchors[900].s - anchors[500].s) * t,
        l: anchors[500].l + (anchors[900].l - anchors[500].l) * t
      };
    }
  }

  const steps = [50, 100, 200, 300, 400, 500, 600, 700, 800, 900, 950];
  return steps.reduce((palette, step) => {
    const { s, l } = step === 50
      ? { s: saturation * 0.2, l: 97 }
      : step === 950
      ? { s: saturation * 0.5, l: 8 }
      : interpolate(step);
    palette[step] = `hsl(${hue}, ${s.toFixed(1)}%, ${l.toFixed(1)}%)`;
    return palette;
  }, {});
}

// Exemple : palette bleue
const blue = generatePalette(214, 70);
```

---

## Rotation de teinte pour la profondeur

HSL standard a un défaut : à luminosité égale, le bleu semble plus sombre que le jaune. Pour conserver la **vivacité perçue** en assombrissant ou éclaircissant :

### Règle de rotation

```
Pour éclaircir → pivoter la teinte vers 60° (jaune), 180° (cyan), ou 300° (magenta)
Pour assombrir → pivoter la teinte vers 0° (rouge), 120° (vert), ou 240° (bleu)
```

Ne jamais dépasser **20-30°** de rotation ou la couleur semble être une autre couleur.

```javascript
function shiftHue(baseHue, lightness, targetLightness) {
  const diff = targetLightness - lightness;
  // Décalage de teinte proportionnel à la variation de luminosité
  const hueShift = diff > 0 ? -diff * 0.5 : -diff * 0.3;
  return ((baseHue + hueShift) % 360 + 360) % 360;
}
```

---

## OKLCH : le modèle supérieur

HSL a une limitation fondamentale : il n'est pas **perceptuellement uniforme**. Deux couleurs à même lightness HSL peuvent avoir des brillances très différentes.

**OKLCH** (`oklch(L C H)`) résout ce problème :
- `L` : luminosité perçue (0-1, linéaire)
- `C` : chroma / saturation (0+)
- `H` : teinte (0-360°)

```css
/* HSL — bleu et jaune semblent différents à même lightness */
hsl(240, 80%, 50%)  /* bleu — semble sombre */
hsl(60,  80%, 50%)  /* jaune — semble brillant */

/* OKLCH — brillance perçue réellement identique */
oklch(0.55 0.2 264)  /* bleu */
oklch(0.85 0.18 100) /* jaune — L différent car jaune est intrinsèquement clair */
```

### Recommandation pratique
- Utiliser **HSL** pour les tokens et la génération de palette (compatibilité universelle)
- Utiliser **OKLCH** pour les ajustements fins de contraste perçu (navigateurs modernes)

---

## Calcul des variantes d'état (hover/active/disabled)

### Formules HSL

```javascript
function stateVariants(h, s, l) {
  return {
    default:  `hsl(${h}, ${s}%, ${l}%)`,
    hover:    `hsl(${h}, ${s}%, ${Math.max(0, l - 8)}%)`,
    active:   `hsl(${h}, ${s}%, ${Math.max(0, l - 15)}%)`,
    focus:    `hsl(${h}, ${s}%, ${l}%)`,  // même couleur + ring
    disabled: `hsl(${h}, ${Math.round(s * 0.4)}%, ${l + 20}%)`,
  };
}

// Exemple : bouton bleu hsl(214, 70%, 50%)
stateVariants(214, 70, 50);
// default:  hsl(214, 70%, 50%)
// hover:    hsl(214, 70%, 42%)
// active:   hsl(214, 70%, 35%)
// disabled: hsl(214, 28%, 70%)
```

### En CSS avec relative colors (modern)

```css
:root {
  --btn-bg: hsl(214, 70%, 50%);
}

.btn:hover  { background: hsl(from var(--btn-bg) h s calc(l - 8)); }
.btn:active { background: hsl(from var(--btn-bg) h s calc(l - 15)); }
```

---

## Dark Mode : HSL Mirroring

Pour un dark mode cohérent, ne pas simplement inverser les couleurs. Utiliser une stratégie de décalage :

### Formule de mirroring

```javascript
function darkModeVariant(h, s, l) {
  return {
    // Décaler la teinte de 15-30° pour un rendu plus atmosphérique
    hue: h + 15,
    // Réduire la saturation de 10-30%
    saturation: Math.round(s * 0.75),
    // Inverser la luminosité autour du centre (50%)
    lightness: 100 - l
  };
}
```

### Application concrète

```css
:root {
  /* Light mode */
  --gray-50:  hsl(220, 20%, 98%);
  --gray-900: hsl(220, 16%, 10%);
  --color-bg: var(--gray-50);
  --color-text: var(--gray-900);
}

[data-theme="dark"] {
  /* Dark mode — pas une inversion brutale */
  --color-bg:   hsl(235, 12%, 10%);  /* teinte décalée, saturation réduite */
  --color-text: hsl(220, 15%, 90%);  /* pas blanc pur */

  /* Les couleurs brand se désaturent légèrement */
  --color-brand: hsl(214, 55%, 60%); /* saturation -15%, lightness +10% */
}
```
