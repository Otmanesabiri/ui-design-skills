# 15 — Mathématiques & Interactions JavaScript

Source : Math for Web Design — Paul McFedries

---

## Lerp (Linear Interpolation)

La formule la plus utilisée en interactions web.

### Formule

```
lerp(a, b, t) = a + (b - a) * t
```

- `a` : valeur de départ
- `b` : valeur d'arrivée
- `t` : facteur d'interpolation (0 = départ, 1 = arrivée)

### Implémentation

```javascript
const lerp = (a, b, t) => a + (b - a) * t;

// Exemples
lerp(0, 100, 0)    // → 0   (départ)
lerp(0, 100, 0.5)  // → 50  (milieu)
lerp(0, 100, 1)    // → 100 (arrivée)
lerp(0, 100, 0.25) // → 25  (25% du chemin)
```

### Application : smooth follow (cursor tracking)

```javascript
let currentX = 0;
let currentY = 0;
let targetX = 0;
let targetY = 0;

document.addEventListener('mousemove', (e) => {
  targetX = e.clientX;
  targetY = e.clientY;
});

function animate() {
  // 0.1 = facteur de douceur (plus petit = plus fluide/lent)
  currentX = lerp(currentX, targetX, 0.1);
  currentY = lerp(currentY, targetY, 0.1);

  cursor.style.transform = `translate(${currentX}px, ${currentY}px)`;
  requestAnimationFrame(animate);
}
animate();
```

### Application : smooth scroll indicator

```javascript
let currentProgress = 0;

function updateProgress() {
  const scrollTop = window.scrollY;
  const maxScroll = document.body.scrollHeight - window.innerHeight;
  const targetProgress = scrollTop / maxScroll; // 0 à 1

  currentProgress = lerp(currentProgress, targetProgress, 0.08);
  progressBar.style.width = `${currentProgress * 100}%`;

  requestAnimationFrame(updateProgress);
}
updateProgress();
```

---

## Mapping de valeurs

Transformer une plage d'entrée vers une plage de sortie.

### Formule

```
map(value, inMin, inMax, outMin, outMax) =
  outMin + (value - inMin) / (inMax - inMin) * (outMax - outMin)
```

### Implémentation

```javascript
function map(value, inMin, inMax, outMin, outMax) {
  return outMin + (value - inMin) / (inMax - inMin) * (outMax - outMin);
}

// Clamp optionnel pour rester dans la plage de sortie
function mapClamped(value, inMin, inMax, outMin, outMax) {
  const mapped = map(value, inMin, inMax, outMin, outMax);
  return Math.min(Math.max(mapped, outMin), Math.max(outMin, outMax));
}
```

### Exemples concrets

```javascript
// Position souris (0 → 1280px) → rotation card (-15° → +15°)
document.addEventListener('mousemove', (e) => {
  const rotation = map(e.clientX, 0, window.innerWidth, -15, 15);
  card.style.transform = `rotateY(${rotation}deg)`;
});

// Scroll (0% → 100%) → opacité hero (1 → 0)
window.addEventListener('scroll', () => {
  const scrollPct = window.scrollY / (document.body.scrollHeight - window.innerHeight);
  const opacity = mapClamped(scrollPct, 0, 0.3, 1, 0);
  hero.style.opacity = opacity;
});

// Scroll → scale navbar (1 → 0.9)
window.addEventListener('scroll', () => {
  const scale = mapClamped(window.scrollY, 0, 100, 1, 0.9);
  navbar.style.transform = `scale(${scale})`;
});
```

---

## Vélocité de scroll

### Calcul simple (progression globale)

```javascript
function getScrollProgress() {
  const scrollTop = window.scrollY;
  const maxScroll = document.body.scrollHeight - window.innerHeight;
  return scrollTop / maxScroll; // 0 à 1
}
```

### Calcul de la vélocité instantanée

```javascript
let lastScrollY = 0;
let lastTime = Date.now();
let velocity = 0;

window.addEventListener('scroll', () => {
  const now = Date.now();
  const dt = now - lastTime;
  const dy = window.scrollY - lastScrollY;

  velocity = dy / dt; // px/ms

  lastScrollY = window.scrollY;
  lastTime = now;
});
```

### Parallax basé sur le scroll

```javascript
function initParallax(element, speed = 0.5) {
  window.addEventListener('scroll', () => {
    const scrolled = window.scrollY;
    // speed : 0 = fixe, 1 = scroll normal, 0.5 = demi-vitesse
    const offset = scrolled * speed;
    element.style.transform = `translateY(${offset}px)`;
  });
}

// Usage
initParallax(document.querySelector('.hero-bg'), 0.3);
```

---

## Intersection Observer + Math

```javascript
function animateOnScroll(elements, options = {}) {
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        // Calculer le délai selon la position dans le groupe
        const index = [...elements].indexOf(entry.target);
        const delay = index * 80; // stagger de 80ms entre chaque élément

        entry.target.style.transitionDelay = `${delay}ms`;
        entry.target.classList.add('visible');
        observer.unobserve(entry.target);
      }
    });
  }, { threshold: 0.15, ...options });

  elements.forEach(el => observer.observe(el));
}

animateOnScroll(document.querySelectorAll('.card'));
```

---

## requestAnimationFrame : pattern correct 60fps

```javascript
class Animator {
  constructor(updateFn) {
    this.updateFn = updateFn;
    this.rafId = null;
    this.lastTime = null;
  }

  start() {
    const tick = (timestamp) => {
      if (this.lastTime === null) this.lastTime = timestamp;
      const dt = timestamp - this.lastTime; // delta time en ms
      this.lastTime = timestamp;

      this.updateFn(dt, timestamp);
      this.rafId = requestAnimationFrame(tick);
    };
    this.rafId = requestAnimationFrame(tick);
  }

  stop() {
    if (this.rafId) cancelAnimationFrame(this.rafId);
    this.rafId = null;
    this.lastTime = null;
  }
}

// Usage
const animator = new Animator((dt, time) => {
  // dt = temps écoulé depuis la dernière frame (ms)
  // Utiliser dt pour des animations indépendantes du framerate
  const y = 20 * Math.sin(time * 0.002);
  element.style.transform = `translateY(${y}px)`;
});

animator.start();
```

---

## Mouse tracking : rotation 3D de carte

```javascript
function init3DCard(card) {
  const MAX_ROTATION = 15; // degrés

  card.addEventListener('mousemove', (e) => {
    const rect = card.getBoundingClientRect();

    // Position relative au centre de la carte (-1 à +1)
    const xRelative = (e.clientX - rect.left - rect.width / 2) / (rect.width / 2);
    const yRelative = (e.clientY - rect.top - rect.height / 2) / (rect.height / 2);

    // Mapper vers la rotation
    const rotateY = map(xRelative, -1, 1, -MAX_ROTATION, MAX_ROTATION);
    const rotateX = map(yRelative, -1, 1, MAX_ROTATION, -MAX_ROTATION);

    card.style.transform = `perspective(1000px) rotateX(${rotateX}deg) rotateY(${rotateY}deg)`;
  });

  card.addEventListener('mouseleave', () => {
    card.style.transform = 'perspective(1000px) rotateX(0deg) rotateY(0deg)';
  });
}
```

---

## Debounce & Throttle : mathématique du timing

### Debounce — déclencher après N ms d'inactivité

```javascript
function debounce(fn, delay = 300) {
  let timer;
  return (...args) => {
    clearTimeout(timer);
    timer = setTimeout(() => fn(...args), delay);
  };
}

// Usage : resize, search input
window.addEventListener('resize', debounce(() => {
  recalculateLayout();
}, 200));
```

### Throttle — déclencher au maximum toutes les N ms

```javascript
function throttle(fn, limit = 16) { // 16ms ≈ 60fps
  let lastTime = 0;
  return (...args) => {
    const now = Date.now();
    if (now - lastTime >= limit) {
      lastTime = now;
      fn(...args);
    }
  };
}

// Usage : scroll, mousemove
window.addEventListener('scroll', throttle(() => {
  updateParallax();
}, 16));
```
