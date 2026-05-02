# 17 — Internationalisation (i18n) & RTL

Sources : Practical UI (Dannaway) · Postel's Law (Laws of UX) · MDN Web Docs

---

## Stress Testing typographique

Un design validé en français ou anglais peut se casser dans d'autres langues. Tester systématiquement avant de livrer.

### Expansion du texte par langue

| Langue | Expansion moyenne vs anglais |
|--------|------------------------------|
| Allemand | +30 à +40% |
| Finnois | +30 à +40% |
| Russe | +20 à +30% |
| Espagnol | +15 à +25% |
| Français | +15 à +20% |
| Anglais | référence (0%) |
| Chinois | -30 à -40% |
| Japonais | -20 à -30% |

### Pseudo-localisation : tester sans traduction réelle

```javascript
// Remplacer le texte par une version allongée artificiellement
function pseudoLocalize(text) {
  const expansion = 1.4; // +40% (cas allemand)
  const padding = 'xxxxxx'.repeat(Math.ceil((text.length * expansion - text.length) / 6));
  return `[${text}${padding}]`;
}

pseudoLocalize("Save")    // → "[Savexxxxxx]"
pseudoLocalize("Submit")  // → "[Submitxxxxxxx]"
```

### Règles pour les composants extensibles

```css
/* MAUVAIS : largeur fixe qui coupe le texte */
.btn { width: 120px; }

/* BON : largeur min + expansion naturelle */
.btn {
  min-width: 120px;
  width: fit-content;
  max-width: 100%;
  white-space: nowrap;       /* éviter le wrapping inattendu */
  overflow: hidden;
  text-overflow: ellipsis;   /* fallback si vraiment trop long */
}

/* Containers de labels */
.label {
  min-width: 0;              /* permet la contraction dans flexbox */
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}
```

---

## Architecture RTL (Right-to-Left)

### Langues RTL concernées
- Arabe (العربية) — 400M+ locuteurs
- Hébreu (עברית)
- Persan/Farsi (فارسی)
- Ourdou (اردو)

### Attribut HTML de base

```html
<!-- Au niveau du document -->
<html lang="ar" dir="rtl">

<!-- Sur un élément spécifique -->
<p dir="rtl">هذا النص بالعربية</p>

<!-- Auto-détection (pas recommandé pour la prod) -->
<p dir="auto">Mixed content</p>
```

### CSS Logical Properties : la bonne approche

Utiliser les **propriétés logiques** au lieu des propriétés directionnelles. Elles s'adaptent automatiquement au `dir`.

```css
/* MAUVAIS : propriétés physiques (ne s'adaptent pas au RTL) */
.element {
  margin-left: 16px;
  padding-right: 24px;
  border-left: 2px solid;
  text-align: left;
}

/* BON : propriétés logiques (RTL-ready automatiquement) */
.element {
  margin-inline-start: 16px;    /* left en LTR, right en RTL */
  padding-inline-end: 24px;     /* right en LTR, left en RTL */
  border-inline-start: 2px solid;
  text-align: start;            /* left en LTR, right en RTL */
}
```

### Table de correspondance logique/physique

| Propriété physique | Propriété logique | Description |
|--------------------|-------------------|-------------|
| `margin-left` | `margin-inline-start` | Début de ligne |
| `margin-right` | `margin-inline-end` | Fin de ligne |
| `margin-top` | `margin-block-start` | Début de bloc |
| `margin-bottom` | `margin-block-end` | Fin de bloc |
| `padding-left` | `padding-inline-start` | |
| `padding-right` | `padding-inline-end` | |
| `border-left` | `border-inline-start` | |
| `border-right` | `border-inline-end` | |
| `left` | `inset-inline-start` | Position |
| `right` | `inset-inline-end` | Position |
| `text-align: left` | `text-align: start` | |
| `text-align: right` | `text-align: end` | |
| `width` | `inline-size` | |
| `height` | `block-size` | |

### Flexbox et Grid : déjà RTL-aware

```css
/* Flexbox respecte automatiquement la direction */
.row {
  display: flex;
  flex-direction: row;     /* row = LTR, row-reverse = RTL géré auto */
  gap: 16px;
  justify-content: flex-start;  /* "start" s'inverse avec RTL */
}

/* Pour les icônes directionnelles (flèches), les inverser en RTL */
[dir="rtl"] .arrow-icon {
  transform: scaleX(-1);
}
```

### Éléments qui ne s'inversent PAS en RTL

Certains éléments gardent leur direction LTR même en RTL :
- Numéros de téléphone
- Adresses email
- URLs
- Code source
- Chiffres (dans la plupart des cas)
- Dates numériques (22/05/2025)

```html
<!-- Forcer LTR pour certains éléments en contexte RTL -->
<span dir="ltr">+212 6 12 34 56 78</span>
<span dir="ltr">user@example.com</span>
```

---

## Nuxt/Vue : implémentation i18n

### Avec `@nuxtjs/i18n`

```typescript
// nuxt.config.ts
export default defineNuxtConfig({
  modules: ['@nuxtjs/i18n'],
  i18n: {
    locales: [
      { code: 'fr', dir: 'ltr', file: 'fr.json' },
      { code: 'ar', dir: 'rtl', file: 'ar.json' },
      { code: 'en', dir: 'ltr', file: 'en.json' }
    ],
    defaultLocale: 'fr'
  }
})
```

```vue
<!-- Appliquer dir dynamiquement sur le html -->
<script setup>
const { localeProperties } = useI18n()
useHead({
  htmlAttrs: {
    lang: () => localeProperties.value.code,
    dir: () => localeProperties.value.dir ?? 'ltr'
  }
})
</script>
```

### Textes qui ne doivent pas être codés en dur

```vue
<!-- MAUVAIS -->
<span>Résultats : {{ count }}</span>

<!-- BON : pluralisation gérée par i18n -->
<span>{{ $t('results', count) }}</span>
```

```json
// fr.json
{
  "results": "Aucun résultat | 1 résultat | {count} résultats"
}
```

---

## Typographie multilingue

### Polices : vérifier le support des caractères

```css
/* Stack de polices avec fallbacks Unicode */
:root {
  font-family:
    'Inter',              /* latin, latin-ext */
    'Noto Sans Arabic',   /* arabe */
    'Noto Sans Hebrew',   /* hébreu */
    system-ui,
    sans-serif;
}

/* Police spécifique pour le contenu RTL */
[dir="rtl"] {
  font-family: 'Noto Sans Arabic', 'Segoe UI', sans-serif;
  line-height: 1.8;  /* l'arabe nécessite plus d'interligne */
}
```

### Line-height pour les langues RTL

L'arabe et le persan ont des diacritiques (harakat) qui nécessitent plus d'espace vertical.

```css
[lang="ar"], [lang="fa"] {
  line-height: 1.8;      /* vs 1.5 en latin */
  letter-spacing: 0;     /* jamais modifier le letter-spacing en arabe */
}
```

---

## Checklist i18n & RTL

```
Texte
[ ] Pas de largeurs fixes sur les composants textuels
[ ] Pseudo-localisation testée (+40% de texte)
[ ] Troncature avec ellipsis en cas de dépassement
[ ] Pluralisation gérée par le système i18n

RTL
[ ] Propriétés logiques utilisées (inline-start/end)
[ ] dir="rtl" défini sur <html> dynamiquement
[ ] Icônes directionnelles inversées en RTL
[ ] Éléments LTR-only marqués avec dir="ltr"
[ ] Layout testé avec du contenu arabe/hébreu réel

Polices
[ ] Stack de polices avec fallbacks Unicode
[ ] Line-height adapté pour les scripts complexes
[ ] letter-spacing = 0 pour les scripts non-latins
```
