# 08 — Design Tokens (Valeurs Concrètes)

Sources : Refactoring UI · Practical UI · Tailwind CSS conventions

---

## Utilisation

Ce fichier contient des valeurs numériques prêtes à l'emploi.
Adapter les teintes (hue) à la couleur brand du projet.

---

## Couleurs

### Gris (teintés bleu — cool gray)

```css
:root {
  --gray-50:  hsl(220, 20%, 98%);   /* fond de page */
  --gray-100: hsl(220, 16%, 95%);   /* fond de section alternative */
  --gray-200: hsl(220, 14%, 90%);   /* bordures légères */
  --gray-300: hsl(220, 12%, 80%);   /* bordures normales */
  --gray-400: hsl(220, 10%, 68%);   /* placeholder text */
  --gray-500: hsl(220, 9%,  55%);   /* texte tertiaire */
  --gray-600: hsl(220, 10%, 42%);   /* texte secondaire */
  --gray-700: hsl(220, 12%, 30%);   /* texte corps */
  --gray-800: hsl(220, 14%, 20%);   /* texte fort */
  --gray-900: hsl(220, 16%, 10%);   /* texte primaire, quasi-noir */
}
```

### Gris chauds (pour les interfaces warm)

```css
:root {
  --warm-gray-50:  hsl(30, 20%, 98%);
  --warm-gray-100: hsl(30, 16%, 95%);
  --warm-gray-200: hsl(30, 14%, 90%);
  --warm-gray-300: hsl(30, 12%, 80%);
  --warm-gray-400: hsl(30, 10%, 68%);
  --warm-gray-500: hsl(30, 9%,  55%);
  --warm-gray-600: hsl(30, 10%, 42%);
  --warm-gray-700: hsl(30, 12%, 30%);
  --warm-gray-800: hsl(30, 14%, 20%);
  --warm-gray-900: hsl(30, 16%, 10%);
}
```

### Bleu (couleur brand par défaut)

```css
:root {
  --blue-50:  hsl(214, 100%, 97%);
  --blue-100: hsl(214, 95%,  92%);
  --blue-200: hsl(214, 90%,  85%);
  --blue-300: hsl(214, 82%,  74%);
  --blue-400: hsl(214, 74%,  62%);
  --blue-500: hsl(214, 70%,  50%);  /* base bouton */
  --blue-600: hsl(214, 72%,  42%);  /* hover */
  --blue-700: hsl(214, 75%,  34%);  /* active / pressed */
  --blue-800: hsl(214, 78%,  24%);  /* text on light */
  --blue-900: hsl(214, 82%,  16%);  /* dark text */
}
```

### Couleurs sémantiques

```css
:root {
  /* Succès */
  --success-50:  hsl(142, 80%, 96%);
  --success-100: hsl(142, 70%, 88%);
  --success-500: hsl(142, 65%, 42%);
  --success-700: hsl(142, 70%, 28%);

  /* Erreur */
  --error-50:  hsl(0, 90%, 97%);
  --error-100: hsl(0, 80%, 90%);
  --error-500: hsl(0, 72%, 50%);
  --error-700: hsl(0, 78%, 35%);

  /* Avertissement */
  --warning-50:  hsl(38, 100%, 96%);
  --warning-100: hsl(38, 95%,  88%);
  --warning-500: hsl(38, 90%,  50%);
  --warning-700: hsl(38, 80%,  32%);

  /* Information */
  --info-50:  hsl(200, 90%, 96%);
  --info-100: hsl(200, 80%, 88%);
  --info-500: hsl(200, 75%, 46%);
  --info-700: hsl(200, 80%, 30%);
}
```

---

## Espacement

```css
:root {
  --space-px:  1px;
  --space-0-5: 2px;
  --space-1:   4px;
  --space-2:   8px;
  --space-3:   12px;
  --space-4:   16px;
  --space-5:   20px;
  --space-6:   24px;
  --space-7:   28px;
  --space-8:   32px;
  --space-10:  40px;
  --space-12:  48px;
  --space-14:  56px;
  --space-16:  64px;
  --space-20:  80px;
  --space-24:  96px;
  --space-32:  128px;
  --space-40:  160px;
  --space-48:  192px;
  --space-64:  256px;
}
```

---

## Typographie

### Échelle de tailles

```css
:root {
  --text-xs:   12px;   /* 0.75rem  — captions, labels minuscules */
  --text-sm:   14px;   /* 0.875rem — helper text, small */
  --text-base: 16px;   /* 1rem     — corps de texte */
  --text-lg:   18px;   /* 1.125rem — corps large */
  --text-xl:   20px;   /* 1.25rem  — lead, intro */
  --text-2xl:  24px;   /* 1.5rem   — H4, sous-titre */
  --text-3xl:  30px;   /* 1.875rem — H3 */
  --text-4xl:  36px;   /* 2.25rem  — H2 */
  --text-5xl:  48px;   /* 3rem     — H1 */
  --text-6xl:  60px;   /* 3.75rem  — Hero */
  --text-7xl:  72px;   /* 4.5rem   — Display */
}
```

### Poids

```css
:root {
  --font-normal:   400;
  --font-medium:   500;
  --font-semibold: 600;
  --font-bold:     700;
  --font-extrabold:800;
}
```

### Line-height

```css
:root {
  --leading-none:    1;
  --leading-tight:   1.25;
  --leading-snug:    1.375;
  --leading-normal:  1.5;
  --leading-relaxed: 1.625;
  --leading-loose:   2;
}

/* Application contextuelle */
.display-text { line-height: var(--leading-none); }    /* 72px+ */
.heading      { line-height: var(--leading-tight); }   /* 30-60px */
.subheading   { line-height: var(--leading-snug); }    /* 24-30px */
.body         { line-height: var(--leading-normal); }  /* 14-20px */
.small        { line-height: var(--leading-relaxed); } /* 12-14px */
```

---

## Ombres

```css
:root {
  --shadow-xs:
    0 1px 2px hsla(220, 15%, 5%, 0.04);

  --shadow-sm:
    0 1px 3px hsla(220, 15%, 5%, 0.06),
    0 1px 2px hsla(220, 15%, 5%, 0.04);

  --shadow-md:
    0 2px 4px hsla(220, 15%, 5%, 0.06),
    0 4px 6px hsla(220, 15%, 5%, 0.06);

  --shadow-lg:
    0 4px 8px hsla(220, 15%, 5%, 0.06),
    0 8px 16px hsla(220, 15%, 5%, 0.08);

  --shadow-xl:
    0 8px 16px hsla(220, 15%, 5%, 0.08),
    0 20px 40px hsla(220, 15%, 5%, 0.12);

  --shadow-2xl:
    0 16px 32px hsla(220, 15%, 5%, 0.10),
    0 40px 80px hsla(220, 15%, 5%, 0.16);

  --shadow-inner:
    inset 0 2px 4px hsla(220, 15%, 5%, 0.08);

  --shadow-none: none;
}

/* Usage par composant */
/* button default    → --shadow-sm */
/* button hover      → --shadow-md */
/* card              → --shadow-sm ou --shadow-md */
/* dropdown          → --shadow-lg */
/* modal             → --shadow-xl */
/* drawer            → --shadow-2xl */
/* input inset       → --shadow-inner */
```

---

## Border-radius

```css
:root {
  --radius-none: 0;
  --radius-sm:   2px;   /* badges compacts, tags */
  --radius-base: 4px;   /* inputs, boutons sm */
  --radius-md:   6px;   /* boutons, cards compactes */
  --radius-lg:   8px;   /* cards, modales */
  --radius-xl:   12px;  /* grandes cards, drawers */
  --radius-2xl:  16px;  /* sheets mobile, hero cards */
  --radius-3xl:  24px;  /* elements marketing */
  --radius-full: 9999px;/* pills, avatars, loaders circulaires */
}
```

---

## Z-Index

```css
:root {
  --z-below:   -1;
  --z-base:     0;
  --z-raised:   1;    /* cartes hover, éléments légèrement surélevés */
  --z-dropdown: 10;   /* dropdowns, menus contextuels */
  --z-sticky:   20;   /* headers sticky, sidebars fixed */
  --z-overlay:  30;   /* overlays d'arrière-plan */
  --z-modal:    40;   /* modales, drawers */
  --z-toast:    50;   /* notifications, toasts */
  --z-tooltip:  60;   /* tooltips */
  --z-top:      9999; /* éléments vraiment au-dessus de tout */
}
```

---

## Transitions & Animations (Loi de Doherty)

Le mouvement doit être intentionnel, rapide (sous les 400ms pour garder l'attention), et guider l'utilisateur.

```css
:root {
  /* Durées (Doherty Threshold : l'interface doit répondre en < 400ms) */
  --duration-fast:    100ms;  /* Micro-interactions: hover, toggle */
  --duration-base:    150ms;  /* Standard: boutons, inputs, couleurs */
  --duration-slow:    200ms;  /* Mouvement physique: cartes, petits déplacements */
  --duration-slower:  300ms;  /* Entrées de composants: modales, popovers */
  --duration-slowest: 500ms;  /* Grands changements de page (rare) */

  /* Easing */
  --ease-in:       cubic-bezier(0.4, 0, 1, 1);         /* Pour sortir de l'écran */
  --ease-out:      cubic-bezier(0, 0, 0.2, 1);         /* Pour entrer dans l'écran */
  --ease-in-out:   cubic-bezier(0.4, 0, 0.2, 1);       /* Pour bouger sur l'écran */
  --ease-spring:   cubic-bezier(0.34, 1.56, 0.64, 1);  /* Légère élasticité (cartes, modals) */
}

/* Transitions standard par type */
.btn         { transition: background var(--duration-base) var(--ease-out),
                           box-shadow var(--duration-base) var(--ease-out),
                           transform var(--duration-fast) var(--ease-out); }
.btn:active  { transform: scale(0.97); } /* Micro-animation de clic */

.input       { transition: border-color var(--duration-base) var(--ease-out),
                           box-shadow var(--duration-base) var(--ease-out); }
.card        { transition: transform var(--duration-slow) var(--ease-spring),
                           box-shadow var(--duration-slow) var(--ease-spring); }
.card:hover  { transform: translateY(-2px); }

.modal       { transition: opacity var(--duration-slower) var(--ease-out),
                           transform var(--duration-slower) var(--ease-spring); }
```

---

## Breakpoints

```css
/* Mobile-first */
:root {
  --bp-sm:  640px;   /* Petites tablettes, grands téléphones paysage */
  --bp-md:  768px;   /* Tablettes */
  --bp-lg:  1024px;  /* Petits laptops */
  --bp-xl:  1280px;  /* Laptops standard */
  --bp-2xl: 1536px;  /* Grands écrans */
}

/* En Tailwind : sm: md: lg: xl: 2xl: */
```

---

## Tokens sémantiques (couche abstraite)

Définir des tokens sémantiques au-dessus des tokens primitifs :

```css
:root {
  /* Surfaces */
  --color-bg-page:      var(--gray-50);
  --color-bg-card:      white;
  --color-bg-input:     white;
  --color-bg-disabled:  var(--gray-100);

  /* Textes */
  --color-text-primary:   var(--gray-900);
  --color-text-secondary: var(--gray-600);
  --color-text-tertiary:  var(--gray-500);
  --color-text-disabled:  var(--gray-400);
  --color-text-inverse:   white;

  /* Bordures */
  --color-border-strong:  var(--gray-300);
  --color-border-normal:  var(--gray-200);
  --color-border-subtle:  var(--gray-100);

  /* Brand */
  --color-brand:          var(--blue-500);
  --color-brand-hover:    var(--blue-600);
  --color-brand-active:   var(--blue-700);
  --color-brand-subtle:   var(--blue-50);

  /* États */
  --color-success:        var(--success-500);
  --color-error:          var(--error-500);
  --color-warning:        var(--warning-500);
  --color-info:           var(--info-500);
}
```