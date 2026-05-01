# 15 — Mathematics & Interactions

Source: Math for Web Design — Paul McFedries

---

## Linear Interpolation (Lerp)

Lerp allows finding a value between two points `a` and `b` based on a percentage `t` (0 to 1).

### Formula
```
value = a + (b - a) * t
```

### Usage: Smooth Scroll / Smooth Cursor
```javascript
let current = 0;
let target = 100;
const ease = 0.1; // 10% movement per frame

function animate() {
  current += (target - current) * ease;
  element.style.transform = `translateX(${current}px)`;
  requestAnimationFrame(animate);
}
```

---

## Mapping: Converting Ranges

Convert a value from one range `[min1, max1]` to another `[min2, max2]`.

### Formula
```javascript
function map(value, min1, max1, min2, max2) {
  return min2 + (max2 - min2) * (value - min1) / (max1 - min1);
}
```

### Usage: Parallax / Scroll effect
Convert scroll percentage (0-100%) to a rotation or displacement.

```javascript
window.addEventListener('scroll', () => {
  const scrollY = window.scrollY;
  const rotation = map(scrollY, 0, 1000, 0, 45); // 0 to 45 degrees over 1000px
  card.style.transform = `rotate(${rotation}deg)`;
});
```

---

## Velocity and Inertia

Calculate velocity to apply an inertia effect after a drag.

### Formula
```
velocity = (currentPos - previousPos) / deltaTime
```

### Inertia Algorithm
```javascript
let velocity = 0;
let position = 0;
const friction = 0.95;

function applyInertia() {
  position += velocity;
  velocity *= friction; // Damping
  
  if (Math.abs(velocity) > 0.1) {
    requestAnimationFrame(applyInertia);
  }
}
```

---

## Distance Calculation (Pythagoras)

Essential for proximity effects (e.g., an element that reacts when the cursor approaches).

### Formula
```
distance = sqrt((x2 - x1)² + (y2 - y1)²)
```

### Usage: Hover Effect with Radius
```javascript
const rect = element.getBoundingClientRect();
const centerX = rect.left + rect.width / 2;
const centerY = rect.top + rect.height / 2;

const dist = Math.sqrt(
  Math.pow(mouseX - centerX, 2) + 
  Math.pow(mouseY - centerY, 2)
);

// Scale according to distance (max effect at 0px, no effect at 200px)
const scale = Math.max(1, 1.2 - dist / 1000);
element.style.transform = `scale(${scale})`;
```

---

## Clamping (JavaScript)

To restrict a value between a minimum and a maximum.

```javascript
const clamp = (val, min, max) => Math.min(Math.max(val, min), max);

// Usage: restrict a card's movement within a container
const newX = clamp(mouseX, 0, containerWidth - cardWidth);
```

---

## Elastic Mapping (Rubber Banding)

Effect used on iOS when reaching the end of a scroll. The movement continues but is slowed down.

### Formula
```javascript
function rubberBand(distance, dimension) {
  return (distance * dimension * 0.5) / (distance + dimension * 0.5);
}
```
If you pull 100px past the limit, the visual displacement will only be ~30px.
