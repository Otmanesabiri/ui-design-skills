# 14 — Mathématiques & Animations

Source : Math for Web Design — Paul McFedries

---

## Cubic Bezier : anatomie

```css
transition-timing-function: cubic-bezier(x1, y1, x2, y2);
```

Les 4 paramètres définissent deux points de contrôle d'une courbe de Bézier cubique :
- `(0,0)` et `(1,1)` sont les points fixes (début et fin)
- `(x1,y1)` : premier point de contrôle
- `(x2,y2)` : deuxième point de contrôle

### Correspondances avec les fonctions natives

```css
ease         → cubic-bezier(0.25, 0.1, 0.25, 1.0)
ease-in      → cubic-bezier(0.42, 0, 1.0, 1.0)
ease-out     → cubic-bezier(0, 0, 0.58, 1.0)
ease-in-out  → cubic-bezier(0.42, 0, 0.58, 1.0)
linear       → cubic-bezier(0, 0, 1, 1)
```

### Courbes personnalisées recommandées

```css
:root {
  /* Standard — entrée lente, sortie rapide (la plus naturelle) */
  --ease-standard: cubic-bezier(0.4, 0, 0.2, 1);

  /* Decelerate — apparition d'éléments depuis l'extérieur */
  --ease-decelerate: cubic-bezier(0, 0, 0.2, 1);

  /* Accelerate — disparition d'éléments vers l'extérieur */
  --ease-accelerate: cubic-bezier(0.4, 0, 1, 1);

  /* Spring — légère élasticité naturelle */
  --ease-spring: cubic-bezier(0.34, 1.56, 0.64, 1);

  /* Bounce — rebond plus prononcé */
  --ease-bounce: cubic-bezier(0.68, -0.55, 0.27, 1.55);
}
```

---

## Durées : règles mathématiques

### Principe fondamental
La durée doit être proportionnelle à la **distance parcourue** et à la **taille de l'élément**.

```
Durée ↑ quand distance ↑
Durée ↑ quand taille de l'élément ↑
```

### Échelle de durées

```css
:root {
  --duration-instant:  50ms;   /* feedback immédiat (ripple, press) */
  --duration-fast:    100ms;   /* hover states, couleur, opacité */
  --duration-base:    150ms;   /* transitions standard (boutons, inputs) */
  --duration-slow:    200ms;   /* mouvements courts (dropdown open) */
  --duration-slower:  300ms;   /* mouvements moyens (slide, expand) */
  --duration-slowest: 500ms;   /* grandes transitions (page, modal) */
  --duration-enter:   250ms;   /* entrée d'éléments */
  --duration-exit:    200ms;   /* sortie (légèrement plus rapide) */
}
```

### Règle : la sortie est plus rapide que l'entrée
Un élément qui apparaît peut être un peu plus lent (on l'observe).
Un élément qui disparaît doit être rapide (ne pas bloquer l'utilisateur).

```css
.modal-enter { transition: opacity 250ms var(--ease-decelerate),
                           transform 250ms var(--ease-decelerate); }
.modal-exit  { transition: opacity 200ms var(--ease-accelerate),
                           transform 200ms var(--ease-accelerate); }
```

---

## Fonctions trigonométriques pour les animations

### Sinus et cosinus : mouvement cyclique

```javascript
// Animation oscillante (vague, pulsation)
function animate(time) {
  const frequency = 0.002; // cycles par milliseconde
  const amplitude = 20;    // px
  const y = amplitude * Math.sin(frequency * time);

  element.style.transform = `translateY(${y}px)`;
  requestAnimationFrame(animate);
}
requestAnimationFrame(animate);
```

### Rotation orbitale

```javascript
function orbit(time, centerX, centerY, radius) {
  const speed = 0.001;
  const x = centerX + radius * Math.cos(speed * time);
  const y = centerY + radius * Math.sin(speed * time);
  return { x, y };
}
```

---

## Spring Animation : physique naturelle

Une spring animation simule un ressort physique. Les paramètres clés :

| Paramètre | Description | Valeur douce | Valeur énergique |
|-----------|-------------|-------------|-----------------|
| `stiffness` | Rigidité du ressort | 120-200 | 300-500 |
| `damping` | Friction (amortissement) | 20-30 | 10-15 |
| `mass` | Inertie | 1 | 0.5-2 |

### Implémentation native (Web Animations API)

```javascript
element.animate(
  [
    { transform: 'scale(0.8)', opacity: 0 },
    { transform: 'scale(1)',   opacity: 1 }
  ],
  {
    duration: 400,
    easing: 'cubic-bezier(0.34, 1.56, 0.64, 1)', // approximation spring
    fill: 'forwards'
  }
);
```

### Avec une vraie équation de ressort

```javascript
class SpringAnimation {
  constructor({ stiffness = 180, damping = 24, mass = 1 } = {}) {
    this.k = stiffness;
    this.b = damping;
    this.m = mass;
    this.velocity = 0;
    this.position = 0;
  }

  step(target, dt = 16) {
    const force = -this.k * (this.position - target);
    const damping = -this.b * this.velocity;
    const acceleration = (force + damping) / this.m;

    this.velocity += acceleration * (dt / 1000);
    this.position += this.velocity * (dt / 1000);
    return this.position;
  }
}
```

---

## Calcul position dans le temps

```javascript
// Mouvement linéaire
position = startPosition + speed * time;

// Mouvement avec accélération
position = startPosition + (initialVelocity * time) + (0.5 * acceleration * time * time);

// Exemple : balle tombant (gravité = 9.8 m/s²)
function ballPosition(t) {
  return 0 + 0 * t + 0.5 * 9.8 * t * t;
}
```

---

## Transitions par type de propriété

```css
/* Couleur / Opacité — rapides */
.btn { transition: background-color var(--duration-fast) var(--ease-standard),
                   opacity var(--duration-fast) var(--ease-standard); }

/* Transform (translate, scale, rotate) — moyennes */
.card { transition: transform var(--duration-slow) var(--ease-spring); }

/* Layout (width, height, margin) — éviter si possible, coûteux */
.panel { transition: width var(--duration-slower) var(--ease-standard); }

/* Box-shadow — moyen */
.card { transition: box-shadow var(--duration-slow) var(--ease-standard); }
```

### Propriétés à éviter d'animer (performance)
Ces propriétés déclenchent un recalcul du layout (reflow) :
- `width`, `height`, `margin`, `padding`, `top`, `left`

**Préférer :**
- `transform: translateX/Y/Scale` — GPU compositing, 60fps garanti
- `opacity` — GPU compositing
- `clip-path` — acceptable sur Chrome/Firefox modernes

---

## `@keyframes` : contrôle mathématique des étapes

```css
/* Entrée avec spring (approximation CSS) */
@keyframes spring-in {
  0%   { transform: scale(0.6);    opacity: 0; }
  60%  { transform: scale(1.05);   opacity: 1; }
  80%  { transform: scale(0.97);             }
  100% { transform: scale(1);               }
}

/* Pulse avec sinus (approximation par étapes) */
@keyframes pulse {
  0%, 100% { transform: scale(1); }
  50%       { transform: scale(1.05); }
}

/* Shake (erreur de formulaire) */
@keyframes shake {
  0%, 100% { transform: translateX(0); }
  20%       { transform: translateX(-8px); }
  40%       { transform: translateX(8px); }
  60%       { transform: translateX(-5px); }
  80%       { transform: translateX(5px); }
}
```
