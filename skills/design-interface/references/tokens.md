# 08 — Design Tokens (Concrete Values)

Sources: Refactoring UI · Practical UI · Tailwind CSS conventions

---

## Usage

This file contains ready-to-use numerical values.
Adapt tints (hue) to the project's brand color.

---

## Colors

### Grays (blue tinted — cool gray)

```css
:root {
  --gray-50:  hsl(220, 20%, 98%);   /* page background */
  --gray-100: hsl(220, 16%, 95%);   /* alternative section background */
  --gray-200: hsl(220, 14%, 90%);   /* light borders */
  --gray-300: hsl(220, 12%, 80%);   /* normal borders */
  --gray-400: hsl(220, 10%, 68%);   /* placeholder text */
  --gray-500: hsl(220, 9%,  55%);   /* tertiary text */
  --gray-600: hsl(220, 10%, 42%);   /* secondary text */
  --gray-700: hsl(220, 12%, 30%);   /* body text */
  --gray-800: hsl(220, 14%, 20%);   /* strong text */
  --gray-900: hsl(220, 16%, 10%);   /* primary text, quasi-black */
}
```

### Warm Grays (for warm interfaces)

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

### Blue (default brand color)

```css
:root {
  --blue-50:  hsl(214, 100%, 97%);
  --blue-100: hsl(214, 95%,  92%);
  --blue-200: hsl(214, 90%,  85%);
  --blue-300: hsl(214, 82%,  74%);
  --blue-400: hsl(214, 74%,  62%);
  --blue-500: hsl(214, 70%,  50%);  /* button base */
  --blue-600: hsl(214, 72%,  42%);  /* hover */
  --blue-700: hsl(214, 75%,  34%);  /* active / pressed */
  --blue-800: hsl(214, 78%,  24%);  /* text on light */
  --blue-900: hsl(214, 82%,  16%);  /* dark text */
}
```

### Semantic Colors

```css
:root {
  /* Success */
  --success-50:  hsl(142, 80%, 96%);
  --success-100: hsl(142, 70%, 88%);
  --success-500: hsl(142, 65%, 42%);
  --success-700: hsl(142, 70%, 28%);

  /* Error */
  --error-50:  hsl(0, 90%, 97%);
  --error-100: hsl(0, 80%, 90%);
  --error-500: hsl(0, 72%, 50%);
  --error-700: hsl(0, 78%, 35%);

  /* Warning */
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

## Spacing

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

## Typography

### Size Scale

```css
:root {
  --text-xs:   12px;   /* 0.75rem  — captions, tiny labels */
  --text-sm:   14px;   /* 0.875rem — helper text, small */
  --text-base: 16px;   /* 1rem     — body text */
  --text-lg:   18px;   /* 1.125rem — large body */
  --text-xl:   20px;   /* 1.25rem  — lead, intro */
  --text-2xl:  24px;   /* 1.5rem   — H4, subheading */
  --text-3xl:  30px;   /* 1.875rem — H3 */
  --text-4xl:  36px;   /* 2.25rem  — H2 */
  --text-5xl:  48px;   /* 3rem     — H1 */
  --text-6xl:  60px;   /* 3.75rem  — Hero */
  --text-7xl:  72px;   /* 4.5rem   — Display */
}
```

### Weights

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

/* Contextual Application */
.display-text { line-height: var(--leading-none); }    /* 72px+ */
.heading      { line-height: var(--leading-tight); }   /* 30-60px */
.subheading   { line-height: var(--leading-snug); }    /* 24-30px */
.body         { line-height: var(--leading-normal); }  /* 14-20px */
.small        { line-height: var(--leading-relaxed); } /* 12-14px */
```

---

## Shadows

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

/* Usage by component */
/* button default    → --shadow-sm */
/* button hover      → --shadow-md */
/* card              → --shadow-sm or --shadow-md */
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
  --radius-sm:   2px;   /* compact badges, tags */
  --radius-base: 4px;   /* inputs, sm buttons */
  --radius-md:   6px;   /* buttons, compact cards */
  --radius-lg:   8px;   /* cards, modals */
  --radius-xl:   12px;  /* large cards, drawers */
  --radius-2xl:  16px;  /* mobile sheets, hero cards */
  --radius-3xl:  24px;  /* marketing elements */
  --radius-full: 9999px;/* pills, avatars, circular loaders */
}
```

---

## Z-Index

```css
:root {
  --z-below:   -1;
  --z-base:     0;
  --z-raised:   1;    /* hover cards, slightly elevated elements */
  --z-dropdown: 10;   /* dropdowns, context menus */
  --z-sticky:   20;   /* sticky headers, fixed sidebars */
  --z-overlay:  30;   /* background overlays */
  --z-modal:    40;   /* modals, drawers */
  --z-toast:    50;   /* notifications, toasts */
  --z-tooltip:  60;   /* tooltips */
  --z-top:      9999; /* elements really above everything */
}
```

---

## Transitions & Animations (Doherty Law)

Movement must be intentional, fast (under 400ms to keep attention), and guide the user.

```css
:root {
  /* Durations (Doherty Threshold: interface must respond in < 400ms) */
  --duration-fast:    100ms;  /* Micro-interactions: hover, toggle */
  --duration-base:    150ms;  /* Standard: buttons, inputs, colors */
  --duration-slow:    200ms;  /* Physical movement: cards, small displacements */
  --duration-slower:  300ms;  /* Component entries: modals, popovers */
  --duration-slowest: 500ms;  /* Large page changes (rare) */

  /* Easing */
  --ease-in:       cubic-bezier(0.4, 0, 1, 1);         /* For exiting the screen */
  --ease-out:      cubic-bezier(0, 0, 0.2, 1);         /* For entering the screen */
  --ease-in-out:   cubic-bezier(0.4, 0, 0.2, 1);       /* For moving on the screen */
  --ease-spring:   cubic-bezier(0.34, 1.56, 0.64, 1);  /* Slight elasticity (cards, modals) */
}

/* Standard transitions by type */
.btn         { transition: background var(--duration-base) var(--ease-out),
                           box-shadow var(--duration-base) var(--ease-out),
                           transform var(--duration-fast) var(--ease-out); }
.btn:active  { transform: scale(0.97); } /* Micro-click animation */

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
  --bp-sm:  640px;   /* Small tablets, large landscape phones */
  --bp-md:  768px;   /* Tablets */
  --bp-lg:  1024px;  /* Small laptops */
  --bp-xl:  1280px;  /* Standard laptops */
  --bp-2xl: 1536px;  /* Large screens */
}

/* In Tailwind: sm: md: lg: xl: 2xl: */
```

---

## Semantic Tokens (Abstract Layer)

Define semantic tokens above primitive tokens:

```css
:root {
  /* Surfaces */
  --color-bg-page:      var(--gray-50);
  --color-bg-card:      white;
  --color-bg-input:     white;
  --color-bg-disabled:  var(--gray-100);

  /* Texts */
  --color-text-primary:   var(--gray-900);
  --color-text-secondary: var(--gray-600);
  --color-text-tertiary:  var(--gray-500);
  --color-text-disabled:  var(--gray-400);
  --color-text-inverse:   white;

  /* Borders */
  --color-border-strong:  var(--gray-300);
  --color-border-normal:  var(--gray-200);
  --color-border-subtle:  var(--gray-100);

  /* Brand */
  --color-brand:          var(--blue-500);
  --color-brand-hover:    var(--blue-600);
  --color-brand-active:   var(--blue-700);
  --color-brand-subtle:   var(--blue-50);

  /* States */
  --color-success:        var(--success-500);
  --color-error:          var(--error-500);
  --color-warning:        var(--warning-500);
  --color-info:           var(--info-500);
}
```