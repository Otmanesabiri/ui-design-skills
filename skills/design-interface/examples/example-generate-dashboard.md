# Example: Dashboard Generation

**User Request:** "Generate a structure for a SaaS dashboard with an overview of revenue, active users, and a table of the latest transactions."

## Agent Response (Based on UI Skills)

### 0. Page Contract Resolution

- **Confirmed page type:** SaaS Dashboard
- **Implicit sections to build (in order):**
  1. Header (page title + primary action)
  2. KPI Cards (3 max — Revenue, Active Users, Transactions)
  3. Data Table (latest transactions)
  4. Empty/Error states for each data zone
- **No user restriction detected** — full contract applies.

### 1. Analysis and Hierarchy (Grayscale First)
Before applying colors, we structure the view to prioritize information:
1. **Global Titles and Actions:** At the top (H1 + Export button).
2. **KPIs (Key Performance Indicators):** Key metrics at the top for immediate visibility.
3. **Transactions Table:** Below, detailed but airy.

### 2. Token Application
- **Spacing:** Use of `gap-6` (24px) between large sections and `gap-4` (16px) inside cards.
- **Typography:** KPI values use a large font (e.g., `text-3xl`, `font-bold`), secondary text is `text-sm` with a `color-text-secondary` color.
- **Surfaces:** Main background is `color-bg-page`, cards are on `color-bg-card` with a soft `shadow-sm` shadow to create elevation.

### 3. Result (HTML/CSS Structure or Component)
```html
<div class="dashboard-layout" style="background: var(--color-bg-page); padding: var(--space-8);">
  <header style="display: flex; justify-content: space-between; margin-bottom: var(--space-8);">
    <h1 style="font-size: var(--text-2xl); font-weight: 700; color: var(--color-text-primary);">Overview</h1>
    <button style="background: var(--color-brand); color: var(--color-text-inverse); padding: var(--space-2) var(--space-4); border-radius: var(--radius-md);">
      Export Report
    </button>
  </header>
  
  <section class="kpi-grid" style="display: grid; grid-template-columns: repeat(3, 1fr); gap: var(--space-6); margin-bottom: var(--space-8);">
    <div class="kpi-card" style="background: var(--color-bg-card); padding: var(--space-6); border-radius: var(--radius-lg); box-shadow: var(--shadow-sm);">
      <span style="color: var(--color-text-secondary); font-size: var(--text-sm);">Total Revenue</span>
      <p style="color: var(--color-text-primary); font-size: var(--text-3xl); font-weight: 800; margin-top: var(--space-2);">$24,500</p>
    </div>
    <!-- Other KPIs... -->
  </section>
  
  <!-- Table Section... -->
</div>
```

**UX Justification:**
- **Hick's Law:** The number of global actions is limited to one (Export).
- **Chunking:** Statistics are grouped in distinct cards for easy reading.

### 4. Expected Result
Visually, this produces an airy page with a very light gray background (`--color-bg-page`). The page title is clearly visible, as is the primary action button in brand color (`--color-brand`). Below, three white cards (`--color-bg-card`) with rounded corners stand out subtly thanks to a light shadow, each containing a prominent and readable numeric indicator.
