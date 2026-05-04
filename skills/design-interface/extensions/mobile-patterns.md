# Mobile-Specific Patterns

Sources: Apple HIG · Material Design 3 · Baymard Institute (Mobile UX) · Laws of UX (Fitts)

> **Agent Instruction:** Load this file ONLY for mobile-specific design tasks. For touch target rules (44px minimum), see `references/accessibilite-avancee.md`. For fluid sizing, see `references/responsive-math.md`. For CSS values, reference `references/tokens.md`.

---

## Thumb Zone

On mobile, most users hold their phone with one hand. The natural reach of the thumb defines three zones:

```
┌─────────────────────┐
│     Hard to reach    │  ← Top corners: avoid primary actions
│                     │
│   OK but stretch     │  ← Middle area: secondary content
│                     │
│  ██ Easy reach ██   │  ← Bottom 1/3: primary actions here
│  ██████████████████ │
└─────────────────────┘
```

### Rules (Fitts's Law Applied to Mobile)

```
[ ] Primary CTA placed in the bottom 1/3 of the screen
[ ] Critical navigation at the bottom (not top hamburger)
[ ] Destructive actions NOT in the easy-reach zone
[ ] FAB (Floating Action Button) anchored bottom-right
```

---

## Touch Targets

> **Cross-reference:** Full touch target rules and CSS are in `references/accessibilite-avancee.md` (section "Tailles touch et zones cliquables"). Key rule: minimum 44×44px (WCAG 2.5.8).

### Common Violations

| Element | Problem | Fix |
|---------|---------|-----|
| Table row actions | Icons too small (16px) | Padding to 44px target |
| Close button (×) | Tiny in corner | 44px minimum with padding |
| Checkbox/Radio | Label not clickable | Wrap in `<label>` |
| Links in paragraphs | Too close together | Increase line-height to 1.6+ |

---

## Bottom Sheet

### When to Use (instead of Modal)
- Mobile confirmations
- Contextual actions (share, more options)
- Quick forms (1-3 fields)
- Filter panels

### Structure

```html
<div class="bottom-sheet" role="dialog" aria-label="Share options">
  <!-- Drag handle (visual affordance) -->
  <div class="sheet-handle" aria-hidden="true"></div>
  
  <div class="sheet-header">
    <h3>Share transaction</h3>
    <button aria-label="Close" class="sheet-close">×</button>
  </div>
  
  <div class="sheet-body">
    <!-- Content -->
  </div>
</div>

<!-- Overlay -->
<div class="sheet-overlay" aria-hidden="true"></div>
```

### CSS

```css
.bottom-sheet {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  background: var(--color-bg-card);
  border-radius: var(--radius-xl) var(--radius-xl) 0 0;
  box-shadow: var(--shadow-2xl);
  z-index: var(--z-modal);
  max-height: 85vh;
  overflow-y: auto;
  transform: translateY(100%);
  transition: transform var(--duration-slower) var(--ease-spring);
}

.bottom-sheet.open {
  transform: translateY(0);
}

.sheet-handle {
  width: 36px;
  height: 4px;
  background: var(--gray-300);
  border-radius: var(--radius-full);
  margin: 8px auto 0;
}

.sheet-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: var(--space-4) var(--space-5);
  border-bottom: 1px solid var(--color-border-subtle);
}

.sheet-body {
  padding: var(--space-5);
  /* Safe area for iPhone notch/gesture bar */
  padding-bottom: calc(var(--space-5) + env(safe-area-inset-bottom));
}
```

---

## Bottom Navigation

### Rules
```
[ ] Maximum 5 items (Hick's Law)
[ ] Each item has icon + label (never icon-only)
[ ] Active item uses color + filled icon (Von Restorff)
[ ] Bar height: 56-64px minimum
[ ] Respects safe-area-inset-bottom (iPhone gesture bar)
```

### Structure

```html
<nav class="bottom-nav" role="navigation" aria-label="Main">
  <a href="/home" class="bottom-nav-item active" aria-current="page">
    <svg class="bottom-nav-icon" aria-hidden="true"><!-- home --></svg>
    <span class="bottom-nav-label">Home</span>
  </a>
  <a href="/search" class="bottom-nav-item">
    <svg class="bottom-nav-icon" aria-hidden="true"><!-- search --></svg>
    <span class="bottom-nav-label">Search</span>
  </a>
  <a href="/profile" class="bottom-nav-item">
    <svg class="bottom-nav-icon" aria-hidden="true"><!-- user --></svg>
    <span class="bottom-nav-label">Profile</span>
  </a>
</nav>
```

### CSS

```css
.bottom-nav {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  display: flex;
  justify-content: space-around;
  align-items: center;
  height: 56px;
  background: var(--color-bg-card);
  border-top: 1px solid var(--color-border-subtle);
  z-index: var(--z-sticky);
  padding-bottom: env(safe-area-inset-bottom);
}

.bottom-nav-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 2px;
  padding: 6px 16px;
  color: var(--color-text-tertiary);
  text-decoration: none;
  font-size: 11px;
  font-weight: 500;
  min-width: 44px;
  min-height: 44px;
  justify-content: center;
}

.bottom-nav-item.active {
  color: var(--color-brand);
}

.bottom-nav-icon {
  width: 22px;
  height: 22px;
}
```

---

## Mobile Form Optimizations

### Input Types (Correct Keyboard)

```html
<!-- Numeric keyboard for amounts -->
<input type="text" inputmode="decimal" placeholder="0.00" />

<!-- Phone keyboard -->
<input type="tel" autocomplete="tel" />

<!-- Email keyboard (with @ and .) -->
<input type="email" autocomplete="email" />

<!-- URL keyboard -->
<input type="url" inputmode="url" />

<!-- PIN/OTP input -->
<input type="text" inputmode="numeric" pattern="[0-9]*"
       autocomplete="one-time-code" maxlength="6" />
```

### Prevent iOS Zoom on Input Focus

```css
/* iOS zooms on inputs with font-size < 16px */
input, select, textarea {
  font-size: 16px; /* minimum to prevent auto-zoom */
}
```

### Date Picker Strategy

```html
<!-- Use native date picker on mobile — better UX than custom -->
<input type="date"
       min="2020-01-01"
       max="2026-12-31"
       aria-label="Transaction date" />

<!-- For desktop: custom date picker via component library -->
<!-- For mobile: always fall back to native type="date" -->
```

---

## Gestures

### Swipe Actions (Use Sparingly)

```
Rules:
[ ] Swipe actions are SHORTCUTS, never the ONLY way to act
[ ] Always provide a visible alternative (button, menu)
[ ] Show a preview of the action during swipe (color + icon)
[ ] Require full swipe for destructive actions (not partial)

Common patterns:
  ← Swipe left: Delete / Archive (red background)
  → Swipe right: Complete / Approve (green background)
```

### Pull-to-Refresh

```
Rules:
[ ] Only for content that can be refreshed (feeds, lists)
[ ] Show a spinner at the top during refresh
[ ] Provide haptic feedback at pull threshold
[ ] Never use on pages with form inputs (accidental trigger)
```

---

## Safe Areas (Notch & Gesture Bar)

```css
/* Respect iPhone notch and Android cutouts */
.full-screen-content {
  padding-top: env(safe-area-inset-top);
  padding-bottom: env(safe-area-inset-bottom);
  padding-left: env(safe-area-inset-left);
  padding-right: env(safe-area-inset-right);
}

/* Bottom fixed elements MUST account for gesture bar */
.fixed-bottom {
  bottom: 0;
  padding-bottom: calc(var(--space-4) + env(safe-area-inset-bottom));
}

/* Set the viewport correctly */
/* <meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover"> */
```

---

## Checklist

```
Touch
[ ] All interactive elements ≥ 44×44px
[ ] ≥ 8px gap between touch targets
[ ] Primary actions in bottom 1/3 (thumb zone)

Navigation
[ ] Bottom nav with max 5 items, icon + label
[ ] safe-area-inset-bottom respected on fixed elements
[ ] Hamburger menu only if bottom nav is insufficient

Forms
[ ] Correct inputmode on all fields
[ ] font-size ≥ 16px on inputs (prevent iOS zoom)
[ ] Native date picker on mobile

Patterns
[ ] Bottom sheet instead of modal for contextual actions
[ ] Swipe actions have visible alternatives
[ ] Pull-to-refresh only on refreshable content

Layout
[ ] env(safe-area-inset-*) applied to edge-touching elements
[ ] viewport-fit=cover in meta viewport
[ ] No hover-dependent interactions (no hover on mobile)
```
