# Navigation Patterns

Sources: Laws of UX (Jakob, Hick, Fitts) · Nielsen Norman Group · Refactoring UI

> **Agent Instruction:** Load this file ONLY when building navigation. For CSS values (colors, spacing, shadows, radii), always reference `references/tokens.md` — values are NOT duplicated here. For button/link styles, see `references/composants.md`.

---

## Choosing the Right Navigation Pattern

| Pattern | Best For | Max Items | Avoid When |
|---------|----------|-----------|------------|
| **Top Nav (Horizontal)** | Marketing sites, simple SaaS | 5-7 links | > 7 items or deep hierarchy |
| **Sidebar** | Dashboards, admin panels, complex apps | 8-15 grouped | Simple landing pages |
| **Tabs** | Content within a single page/section | 3-6 tabs | > 6 tabs or unrelated content |
| **Bottom Nav (Mobile)** | Mobile-first apps | 3-5 icons | Desktop-only apps |
| **Breadcrumbs** | Deep hierarchies (e-commerce, docs) | Unlimited depth | Flat structures |
| **Command Palette** | Power users, SaaS tools | Unlimited | Consumer-facing simple apps |
| **Mega Menu** | E-commerce with many categories | 3-5 columns | Simple SaaS |

---

## Top Navigation (Header)

### Structure (Jakob's Law)

Users expect: Logo left, links center, actions right.

```html
<header>
  <nav class="top-nav" role="navigation" aria-label="Main navigation">
    <!-- Zone 1: Brand (left) -->
    <a href="/" class="nav-logo" aria-label="Home">Brand</a>

    <!-- Zone 2: Links (center) -->
    <ul class="nav-links" role="list">
      <li><a href="/features" class="nav-link">Features</a></li>
      <li><a href="/pricing" class="nav-link">Pricing</a></li>
      <li><a href="/docs" class="nav-link">Docs</a></li>
    </ul>

    <!-- Zone 3: Actions (right) -->
    <div class="nav-actions">
      <a href="/login" class="btn btn-ghost">Log in</a>
      <a href="/signup" class="btn btn-primary">Start free trial</a>
    </div>
  </nav>
</header>
```

### Scroll Behavior

Apply `position: sticky; top: 0; z-index: var(--z-sticky)` with `backdrop-filter: blur(12px)`. On scroll, toggle a `.scrolled` class that adds `border-bottom-color: var(--color-border-subtle)` and `box-shadow: var(--shadow-sm)`. Use transitions from `tokens.md` (`--duration-base`, `--ease-out`).

```css
/* Key properties only — see tokens.md for all var() values */
.top-nav { position: sticky; top: 0; z-index: var(--z-sticky); backdrop-filter: blur(12px); }
.top-nav.scrolled { border-bottom-color: var(--color-border-subtle); box-shadow: var(--shadow-sm); }
```

```javascript
// Doherty: respond in < 100ms, use passive listener
const nav = document.querySelector('.top-nav');
window.addEventListener('scroll', () => {
  nav.classList.toggle('scrolled', window.scrollY > 60);
}, { passive: true });
```

### Active State

```css
.nav-link {
  color: var(--color-text-secondary);
  font-size: 14px;
  font-weight: 500;
  padding: 8px 12px;
  border-radius: var(--radius-md);
  transition: color var(--duration-base) var(--ease-out),
              background var(--duration-base) var(--ease-out);
}

.nav-link:hover {
  color: var(--color-text-primary);
  background: var(--gray-100);
}

/* Active page — clear visual signal, not just color */
.nav-link[aria-current="page"] {
  color: var(--color-brand);
  font-weight: 600;
  background: var(--color-brand-subtle);
}
```

---

## Sidebar Navigation

### When to Use
- Application has > 5 top-level sections
- Users need persistent navigation context
- Dashboard or admin panel

### Structure

```html
<aside class="sidebar" role="navigation" aria-label="Application navigation">
  <div class="sidebar-header">
    <a href="/" class="sidebar-logo">Brand</a>
  </div>

  <nav class="sidebar-nav">
    <!-- Primary Section -->
    <ul role="list">
      <li>
        <a href="/dashboard" class="sidebar-link active" aria-current="page">
          <svg class="sidebar-icon" aria-hidden="true"><!-- icon --></svg>
          Dashboard
        </a>
      </li>
      <li>
        <a href="/transactions" class="sidebar-link">
          <svg class="sidebar-icon" aria-hidden="true"><!-- icon --></svg>
          Transactions
          <span class="sidebar-badge" aria-label="3 new">3</span>
        </a>
      </li>
    </ul>

    <!-- Section Divider (Miller's Law: group related items) -->
    <div class="sidebar-divider">Settings</div>

    <ul role="list">
      <li>
        <a href="/settings" class="sidebar-link">
          <svg class="sidebar-icon" aria-hidden="true"><!-- icon --></svg>
          Settings
        </a>
      </li>
    </ul>
  </nav>

  <!-- User info at bottom (predictable position) -->
  <div class="sidebar-footer">
    <div class="user-pill">
      <div class="avatar">JD</div>
      <span class="user-name">John Doe</span>
    </div>
  </div>
</aside>
```

### Key CSS Properties

```css
/* Sidebar shell: 260px wide, sticky, full height */
.sidebar { width: 260px; height: 100vh; position: sticky; top: 0; border-right: 1px solid var(--color-border-subtle); }

/* Links: flex row, icon + text, --radius-md, --duration-base transitions */
.sidebar-link { display: flex; align-items: center; gap: var(--space-3); padding: 10px 12px; border-radius: var(--radius-md); font-size: 14px; }
.sidebar-link:hover { background: var(--gray-100); color: var(--color-text-primary); }
.sidebar-link.active { background: var(--color-brand-subtle); color: var(--color-brand); font-weight: 600; }

/* Badge (notification count): pill shape, error color */
.sidebar-badge { margin-left: auto; background: var(--error-500); color: white; font-size: 11px; border-radius: var(--radius-full); }

/* Divider label: uppercase, 11px, --color-text-tertiary */
.sidebar-divider { font-size: 11px; text-transform: uppercase; letter-spacing: 0.08em; color: var(--color-text-tertiary); }
```

### Collapsible Sidebar (Responsive)

```css
/* Collapsed state: icons only */
.sidebar.collapsed {
  width: 64px;
}

.sidebar.collapsed .sidebar-link span,
.sidebar.collapsed .sidebar-divider,
.sidebar.collapsed .user-name {
  display: none;
}

.sidebar.collapsed .sidebar-link {
  justify-content: center;
  padding: 10px;
}

/* Mobile: overlay drawer */
@media (max-width: 768px) {
  .sidebar {
    position: fixed;
    z-index: var(--z-modal);
    transform: translateX(-100%);
    transition: transform var(--duration-slower) var(--ease-out);
  }

  .sidebar.open {
    transform: translateX(0);
  }
}
```

---

## Tabs

### Rules

1. **Max 6 tabs** — beyond that, use a dropdown or sidebar (Hick's Law)
2. **First tab = most used action** — not alphabetical
3. **Active tab must be visually distinct** — not just underline color
4. **Content changes, URL should too** — tabs should be deep-linkable
5. **Never nest tabs inside tabs** — use cards or sections instead

### Structure

```html
<div class="tabs" role="tablist" aria-label="Account settings">
  <button role="tab" aria-selected="true" aria-controls="panel-general" id="tab-general"
          class="tab active">
    General
  </button>
  <button role="tab" aria-selected="false" aria-controls="panel-security" id="tab-security"
          class="tab" tabindex="-1">
    Security
  </button>
  <button role="tab" aria-selected="false" aria-controls="panel-billing" id="tab-billing"
          class="tab" tabindex="-1">
    Billing
  </button>
</div>

<div role="tabpanel" id="panel-general" aria-labelledby="tab-general">
  <!-- Content -->
</div>
<div role="tabpanel" id="panel-security" aria-labelledby="tab-security" hidden>
  <!-- Content -->
</div>
```

### CSS

```css
.tabs {
  display: flex;
  gap: var(--space-1);
  border-bottom: 1px solid var(--color-border-normal);
  padding: 0 var(--space-4);
}

.tab {
  padding: 10px 16px;
  font-size: 14px;
  font-weight: 500;
  color: var(--color-text-secondary);
  border: none;
  background: none;
  cursor: pointer;
  border-bottom: 2px solid transparent;
  margin-bottom: -1px;
  transition: color var(--duration-base) var(--ease-out),
              border-color var(--duration-base) var(--ease-out);
}

.tab:hover {
  color: var(--color-text-primary);
}

.tab.active {
  color: var(--color-brand);
  border-bottom-color: var(--color-brand);
  font-weight: 600;
}
```

### Keyboard Navigation (Required)

```javascript
// Arrow keys navigate between tabs (WAI-ARIA Tabs pattern)
tablist.addEventListener('keydown', (e) => {
  const tabs = [...tablist.querySelectorAll('[role="tab"]')];
  const current = tabs.indexOf(document.activeElement);

  if (e.key === 'ArrowRight') {
    const next = (current + 1) % tabs.length;
    tabs[next].focus();
    tabs[next].click();
  }
  if (e.key === 'ArrowLeft') {
    const prev = (current - 1 + tabs.length) % tabs.length;
    tabs[prev].focus();
    tabs[prev].click();
  }
});
```

---

## Breadcrumbs

### When to Use
- Hierarchical content deeper than 2 levels
- E-commerce category trees
- Documentation sites

### Structure

```html
<nav aria-label="Breadcrumb">
  <ol class="breadcrumbs" role="list">
    <li><a href="/">Home</a></li>
    <li aria-hidden="true" class="separator">/</li>
    <li><a href="/products">Products</a></li>
    <li aria-hidden="true" class="separator">/</li>
    <li><a href="/products/gateways">Gateways</a></li>
    <li aria-hidden="true" class="separator">/</li>
    <li aria-current="page">Forma Pro</li>
  </ol>
</nav>
```

```css
.breadcrumbs {
  display: flex;
  align-items: center;
  gap: var(--space-2);
  font-size: 13px;
  list-style: none;
  padding: 0;
}

.breadcrumbs a {
  color: var(--color-text-secondary);
  text-decoration: none;
}

.breadcrumbs a:hover {
  color: var(--color-brand);
  text-decoration: underline;
}

.breadcrumbs [aria-current="page"] {
  color: var(--color-text-primary);
  font-weight: 500;
}

.separator {
  color: var(--color-text-tertiary);
  font-size: 12px;
}
```

---

## Command Palette (Ctrl+K)

### When to Use
- SaaS applications with many pages/actions
- Power users who prefer keyboard
- Applications with > 10 navigable sections

### Structure

```html
<dialog class="command-palette" id="command-palette" aria-label="Command palette">
  <div class="palette-search">
    <svg class="palette-search-icon" aria-hidden="true"><!-- search icon --></svg>
    <input type="text" placeholder="Type a command or search..."
           aria-label="Search commands" id="palette-input"
           autocomplete="off" />
    <kbd class="palette-shortcut">Esc</kbd>
  </div>
  <div class="palette-results" role="listbox" aria-label="Search results">
    <div class="palette-group">
      <div class="palette-group-label">Pages</div>
      <button role="option" class="palette-item active">
        <svg aria-hidden="true"><!-- icon --></svg>
        <span>Dashboard</span>
        <kbd>↵</kbd>
      </button>
      <button role="option" class="palette-item">
        <svg aria-hidden="true"><!-- icon --></svg>
        <span>Transactions</span>
        <kbd>↵</kbd>
      </button>
    </div>
    <div class="palette-group">
      <div class="palette-group-label">Actions</div>
      <button role="option" class="palette-item">
        <svg aria-hidden="true"><!-- icon --></svg>
        <span>Create new merchant</span>
        <kbd>↵</kbd>
      </button>
    </div>
  </div>
</dialog>
```

```css
.command-palette {
  position: fixed;
  top: 20%;
  left: 50%;
  transform: translateX(-50%);
  width: min(560px, 90vw);
  max-height: 400px;
  background: var(--color-bg-card);
  border: 1px solid var(--color-border-normal);
  border-radius: var(--radius-xl);
  box-shadow: var(--shadow-2xl);
  z-index: var(--z-modal);
  overflow: hidden;
}

.palette-search {
  display: flex;
  align-items: center;
  gap: var(--space-3);
  padding: var(--space-4);
  border-bottom: 1px solid var(--color-border-subtle);
}

.palette-search input {
  flex: 1;
  border: none;
  font-size: 16px;
  background: transparent;
  outline: none;
}

.palette-item {
  display: flex;
  align-items: center;
  gap: var(--space-3);
  padding: 10px var(--space-4);
  width: 100%;
  border: none;
  background: none;
  font-size: 14px;
  color: var(--color-text-primary);
  cursor: pointer;
  border-radius: var(--radius-md);
}

.palette-item.active,
.palette-item:hover {
  background: var(--color-brand-subtle);
  color: var(--color-brand);
}

.palette-group-label {
  font-size: 11px;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  color: var(--color-text-tertiary);
  padding: var(--space-3) var(--space-4) var(--space-1);
}
```

---

## Checklist Navigation

```
Pattern Selection
[ ] Pattern chosen matches content depth and item count
[ ] No more than 7 top-level items in horizontal nav (Hick's Law)
[ ] Sidebar items grouped by theme with dividers (Miller's Law)

Active State
[ ] Current page/section clearly indicated (not just color)
[ ] aria-current="page" on active links
[ ] Active state uses background + color (not underline alone)

Accessibility
[ ] All navigation has aria-label describing its purpose
[ ] Keyboard navigation works (Tab, Arrow keys for tabs)
[ ] Skip link present before main navigation
[ ] Focus trap in mobile drawer/overlay

Responsive
[ ] Sidebar collapses to icons or drawer on mobile
[ ] Top nav converts to hamburger menu below 768px
[ ] Touch targets ≥ 44px on mobile
[ ] Bottom nav items have icon + label (never icon alone)

Scroll
[ ] Header uses sticky positioning
[ ] Scroll handler uses { passive: true }
[ ] Visual feedback on scroll (border, shadow)
```
