# 14 — Mathematics & Animations

Source: Math for Web Design — Paul McFedries

---

## Cubic Bezier: The Curve Geometry

CSS animations use cubic Bezier curves defined by 4 points: `(0,0)`, `P1`, `P2`, and `(1,1)`.

### Common Curves

| Name | CSS Value | Mathematical Feeling |
|---|---|---|
| Ease-in | `cubic-bezier(0.42, 0, 1, 1)` | Starts slow, ends fast |
| Ease-out | `cubic-bezier(0, 0, 0.58, 1)` | Starts fast, ends slow |
| Ease-in-out | `cubic-bezier(0.42, 0, 0.58, 1)` | Slow start and end |
| **Ease-Spring** | `cubic-bezier(0.34, 1.56, 0.64, 1)` | **Bouncy effect (exceeds target)** |

---

## Durations and Doherty Threshold

For an interface to feel "live" and responsive, movement must respect human perception.

| Duration | Perception | Usage |
|---|---|---|
| **100ms** | Instantaneous | Hover, toggle, checkbox |
| **200ms** | Quick | Button press, icon change |
| **300ms** | Natural | Modal entry, dropdown open |
| **500ms+** | Slow | Large page transitions (rare) |

### Règle Doherty
L'interface doit répondre visuellement sous **400ms**. Si une animation dépasse cette durée sans but fonctionnel, elle est perçue comme un ralentissement.

---

## Spring Physics (Mathematical Spring)

CSS `transition` is linear in its duration. For a more "physical" feel, use a spring model.

### Spring Properties
1. **Mass**: weight of the object
2. **Stiffness**: tension of the spring
3. **Damping**: friction that stops movement

### CSS Implementation (Simplified)
```css
.spring-pop {
  transition: transform 400ms cubic-bezier(0.34, 1.56, 0.64, 1);
}
.spring-pop:hover {
  transform: scale(1.1);
}
```

---

## Trigonometry for Circular Movement

To move an element along a circle of radius `R`:

```javascript
function circularPosition(angleDegrees, radius) {
  const angleRad = (angleDegrees * Math.PI) / 180;
  return {
    x: radius * Math.cos(angleRad),
    y: radius * Math.sin(angleRad)
  };
}
```

### Application CSS (Center items around an icon)
```css
.item-1 { transform: translate(calc(cos(0deg) * 100px), calc(sin(0deg) * 100px)); }
.item-2 { transform: translate(calc(cos(45deg) * 100px), calc(sin(45deg) * 100px)); }
```

---

## Sequencing and Delays (Choreography)

To animate a list of items, use a linear delay:

```css
/* n = index of the element */
delay = n * 50ms;
```

```javascript
// JS Generation
items.forEach((item, i) => {
  item.style.transitionDelay = `${i * 50}ms`;
});
```

---

## Staggered Animation Rule

**Maximum 1000ms** for the total duration of a staggered sequence. Beyond that, the user perceives the system as blocked.

```
Total duration = (Number of items × Delay) + Individual duration
Ex: (5 items × 50ms) + 300ms = 550ms (OK ✓)
```
