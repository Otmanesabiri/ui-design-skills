# Search & Filtering Patterns

Sources: NNGroup · Baymard Institute · Laws of UX (Hick, Miller)

> **Agent Instruction:** Load this file ONLY when building search, autocomplete, or filter interfaces. For input CSS styles, see `references/composants.md`. For cognitive load rules, see `references/lois-ux.md`. For CSS values, reference `references/tokens.md`.

---

## Choosing the Right Pattern

| User Intent | Pattern | Example |
|------------|---------|---------|
| Knows exactly what they want | **Search bar** | "Order #9201" |
| Browsing within constraints | **Faceted filters** | Category + Price range |
| Exploring loosely | **Search + suggestions** | "revenue r..." → autocomplete |
| Refining visible data | **Inline table filters** | Column dropdowns |

---

## Search Bar

### Structure

```html
<div class="search-box" role="search">
  <svg class="search-icon" aria-hidden="true"><!-- magnifier --></svg>
  <input
    type="search"
    placeholder="Search transactions..."
    aria-label="Search transactions"
    autocomplete="off"
    id="search-input"
  />
  <!-- Clear button — visible only when input has value -->
  <button class="search-clear" aria-label="Clear search" hidden>
    <svg aria-hidden="true"><!-- × icon --></svg>
  </button>
  <!-- Keyboard shortcut hint -->
  <kbd class="search-shortcut" aria-hidden="true">⌘K</kbd>
</div>
```

### CSS

```css
.search-box {
  display: flex;
  align-items: center;
  gap: var(--space-2);
  padding: 8px 12px;
  border: 1.5px solid var(--color-border-normal);
  border-radius: var(--radius-md);
  background: var(--color-bg-input);
  transition: border-color var(--duration-base) var(--ease-out),
              box-shadow var(--duration-base) var(--ease-out);
}

.search-box:focus-within {
  border-color: var(--color-brand);
  box-shadow: 0 0 0 3px hsla(var(--color-brand-hsl), 0.15);
}

.search-box input {
  flex: 1;
  border: none;
  background: transparent;
  font-size: 14px;
  outline: none;
}

.search-icon {
  width: 16px;
  height: 16px;
  color: var(--color-text-tertiary);
  flex-shrink: 0;
}

.search-shortcut {
  font-size: 11px;
  padding: 2px 6px;
  border: 1px solid var(--color-border-normal);
  border-radius: var(--radius-sm);
  color: var(--color-text-tertiary);
  background: var(--gray-50);
}
```

### Behavior Rules

```
[ ] Debounce input: 300ms minimum before firing search
[ ] Show results after ≥ 2 characters (not 1)
[ ] Clear button appears only when input is non-empty
[ ] Escape key clears input and closes results
[ ] Enter key navigates to first result or submits
[ ] Loading indicator replaces search icon during fetch
```

---

## Autocomplete / Typeahead

### Structure

```html
<div class="autocomplete-wrapper" role="combobox" aria-expanded="true">
  <input type="search" aria-autocomplete="list" aria-controls="results-list" />
  
  <ul id="results-list" class="autocomplete-results" role="listbox">
    <li role="option" class="result-item active" aria-selected="true">
      <span class="result-match">Acme</span> Corp
      <span class="result-meta">Merchant · Active</span>
    </li>
    <li role="option" class="result-item">
      <span class="result-match">Acme</span> Holdings
      <span class="result-meta">Merchant · Pending</span>
    </li>
  </ul>
</div>
```

### Highlighting Matched Text

```css
.result-match {
  font-weight: 700;
  color: var(--color-text-primary);
  /* Do NOT use color alone — also use weight (accessibility rule) */
}

.result-meta {
  font-size: 12px;
  color: var(--color-text-tertiary);
  margin-left: auto;
}
```

### Keyboard Navigation (Required)

```javascript
// Arrow Up/Down: navigate results
// Enter: select highlighted result
// Escape: close dropdown and clear
input.addEventListener('keydown', (e) => {
  if (e.key === 'ArrowDown') {
    e.preventDefault();
    highlightNext();
  }
  if (e.key === 'ArrowUp') {
    e.preventDefault();
    highlightPrev();
  }
  if (e.key === 'Enter') {
    selectHighlighted();
  }
  if (e.key === 'Escape') {
    closeResults();
  }
});
```

---

## Faceted Filters

### When to Use
- E-commerce product listings
- Dashboard data with multiple dimensions
- Any list with > 20 items and > 3 filterable attributes

### Structure

```html
<!-- Filter bar — show active filters as removable tags -->
<div class="filter-bar">
  <button class="btn btn-ghost filter-trigger">
    <svg aria-hidden="true"><!-- filter icon --></svg>
    Filters
    <span class="filter-count" aria-label="2 active filters">2</span>
  </button>

  <!-- Active filter tags -->
  <div class="filter-tags" role="list" aria-label="Active filters">
    <span class="filter-tag" role="listitem">
      Status: Active
      <button aria-label="Remove status filter">×</button>
    </span>
    <span class="filter-tag" role="listitem">
      Amount: > $100
      <button aria-label="Remove amount filter">×</button>
    </span>
    <button class="filter-clear">Clear all</button>
  </div>
</div>
```

### CSS

```css
.filter-tag {
  display: inline-flex;
  align-items: center;
  gap: var(--space-1);
  padding: 4px 8px;
  background: var(--color-brand-subtle);
  color: var(--color-brand);
  border-radius: var(--radius-full);
  font-size: 13px;
  font-weight: 500;
}

.filter-tag button {
  border: none;
  background: none;
  color: inherit;
  cursor: pointer;
  padding: 0 2px;
  font-size: 14px;
  line-height: 1;
}

.filter-count {
  background: var(--color-brand);
  color: white;
  font-size: 11px;
  font-weight: 700;
  padding: 1px 6px;
  border-radius: var(--radius-full);
  min-width: 18px;
  text-align: center;
}
```

### Rules (Hick's Law)

```
[ ] Do NOT show 10 empty filter fields by default
[ ] Use a "Filter" button that opens a panel/popover
[ ] Display active filters as removable tags above the data
[ ] "Clear all" button visible when ≥ 1 filter is active
[ ] Show result count after filtering: "23 results"
[ ] Filter changes apply immediately (no "Apply" button needed)
```

---

## Search Results States

### No Results

```html
<div class="search-empty">
  <svg aria-hidden="true"><!-- empty search icon --></svg>
  <p class="search-empty-title">No results for "xyz"</p>
  <p class="search-empty-hint">Try different keywords or check your spelling.</p>
</div>
```

### Loading

```html
<div class="search-loading" aria-live="polite">
  <div class="skeleton" style="height: 40px; width: 100%;"></div>
  <div class="skeleton" style="height: 40px; width: 100%;"></div>
  <div class="skeleton" style="height: 40px; width: 80%;"></div>
</div>
```

### Error

```html
<div class="search-error" role="alert">
  <p>Search is temporarily unavailable.</p>
  <button onclick="retrySearch()">Try again</button>
</div>
```

---

## Checklist

```
Search Bar
[ ] Debounced input (300ms minimum)
[ ] Clear button visible when non-empty
[ ] Keyboard shortcut (⌘K or Ctrl+K) if applicable
[ ] aria-label on search input

Autocomplete
[ ] Results navigable with Arrow keys
[ ] Matched text highlighted with font-weight (not color alone)
[ ] Maximum 7-10 visible suggestions (Miller's Law)
[ ] Escape closes, Enter selects

Filters
[ ] Active filters shown as removable tags
[ ] "Clear all" available when filters active
[ ] Result count displayed after filtering
[ ] Filter panel hidden by default (Hick's Law)

States
[ ] Empty state with helpful suggestion
[ ] Loading skeleton during fetch
[ ] Error state with retry action
```
