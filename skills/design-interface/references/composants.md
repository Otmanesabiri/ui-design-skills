# 07 — UI Components

Sources: Refactoring UI · Practical UI ch.6 (Forms) · Laws of UX (Fitts, Hick)

---

## Buttons

### Anatomy of a Good Button

```css
.btn-primary {
  /* Structure */
  display: inline-flex;
  align-items: center;
  gap: 8px;

  /* Sizing */
  padding: 10px 20px;
  min-height: 44px;       /* WCAG touch target */
  border-radius: 6px;

  /* Typography */
  font-size: 14px;
  font-weight: 600;
  line-height: 1.2;
  white-space: nowrap;

  /* Color */
  background: var(--color-primary-500);
  color: #fff;
  border: none;

  /* Interaction */
  cursor: pointer;
  transition: background 150ms ease, box-shadow 150ms ease;
}
```

### All States (Mandatory)

| State | Modification |
|------|-------------|
| `default` | Base color, shadow sm |
| `hover` | Color -100 (darker), shadow md |
| `focus` | 2px brand color outline, 2px offset |
| `active` | Color -200, shadow none (sinks) |
| `disabled` | 0.5 opacity, cursor not-allowed, pointer-events none |
| `loading` | Spinner + "..." text or maintain original text |

### Button Sizes

| Size | Padding | Font-size | Usage |
|--------|---------|-----------|-------|
| xs | 4px 10px | 12px | Actions in tables or compact spaces |
| sm | 6px 14px | 13px | Inline secondary actions |
| md | 10px 20px | 14px | Standard button |
| lg | 14px 28px | 16px | Main CTA, forms |
| xl | 18px 36px | 18px | Hero CTA |

### Button Text
- **Precise Action Verb**: "Create an account", "Send report", "Delete file"
- **Not**: "OK", "Submit", "Confirm" (too vague)
- **Capitalization**: Sentence case preferred ("Send"), not ALL CAPS

---

## Forms

### Form Structure

**Optimal element order:**
```
1. Title/context (why this form)
2. Fields grouped by theme
3. Helper text under complex fields
4. Immediate inline validation
5. Submission button (single, primary, bottom right)
6. Secondary action/link (cancel, go back) on the left
```

### Labels

```css
/* Always above the field, not to the left (except special cases) */
.label {
  display: block;
  font-size: 14px;
  font-weight: 500;
  color: hsl(220, 10%, 35%);
  margin-bottom: 6px;
}
```

**Avoid placeholders as only labels** — they disappear as soon as the user starts typing.

### Saisie Fields (inputs)

```css
.input {
  width: 100%;
  padding: 10px 14px;
  font-size: 16px;         /* ≥16px on iOS to avoid automatic zoom */
  border: 1.5px solid hsl(220, 12%, 80%);
  border-radius: 6px;
  background: #fff;
  transition: border-color 150ms;
}

.input:focus {
  outline: none;
  border-color: var(--color-primary-500);
  box-shadow: 0 0 0 3px hsla(var(--color-primary-hsl), 0.15);
}

.input.error {
  border-color: hsl(0, 70%, 55%);
}

.input:disabled {
  background: hsl(220, 13%, 96%);
  cursor: not-allowed;
  opacity: 0.7;
}
```

### Validation and Errors

**Validation Timing:**
- Validate **on blur** (when the user leaves the field), not on keystroke
- Exception: positive feedback (✓) can appear in real-time once the value is valid

**Error Message:**
```html
<div class="field">
  <label for="email">Email</label>
  <input id="email" type="email" aria-describedby="email-error" />
  <p id="email-error" class="error-message" role="alert">
    ✗ Please enter a valid email address
  </p>
</div>
```

```css
.error-message {
  font-size: 13px;
  color: hsl(0, 70%, 50%);
  margin-top: 4px;
  display: flex;
  align-items: center;
  gap: 4px;
}
```

### Multi-step Forms (Hick's Law)

```
Step 1/4 ─────────────────────
Personal Information
  First Name    Last Name
  Email
  
               [Continue →]
```

**Rules:**
- Display step number and total (`Step 2 of 4`)
- Group related fields in the same step
- Allow going back without losing data
- "Continue" button only, no premature "Save"

### Optional Fields

Avoid optional fields. Use **progressive opt-ins**:

```
// BAD
[Phone (optional)]

// GOOD
□ Receive updates by SMS
  If yes → [Phone] (field revealed dynamically)
```

### Important HTML Attributes

```html
<!-- Always specify autocomplete for common fields -->
<input type="email" autocomplete="email" />
<input type="tel" autocomplete="tel" />
<input type="text" autocomplete="given-name" />

<!-- inputmode for adapted mobile keyboard -->
<input type="text" inputmode="numeric" />    <!-- digits only -->
<input type="text" inputmode="decimal" />    <!-- digits + comma -->
<input type="text" inputmode="tel" />        <!-- phone keyboard -->
<input type="text" inputmode="email" />      <!-- email keyboard (@, .) -->
```

---

## Data Tables and Complex Components

For very dense views (Dashboards, Tables with >10 columns), apply **Miller's Law**: humans can only process ~7 items at a time. The solution is *Chunking* (visual grouping).

### Chunking (Grouping) in Tables
Instead of adding one column per piece of data, merge related data:
```html
<!-- BEFORE: 3 columns (Avatar | Name | Email) -->

<!-- AFTER: 1 column (User) -->
<td class="user-cell">
  <img src="avatar.jpg" class="avatar" />
  <div class="user-info">
    <span class="name">Jane Doe</span>
    <span class="email text-secondary">jane@example.com</span>
  </div>
</td>
```

### Alignment

| Data Type | Alignment |
|---|---|
| Text, Users, Links | Left |
| Numbers, amounts, dates | **Right** (facilitates visual comparison) |
| Status, badges, icons | Center |
| Actions (buttons, `...` menu) | Center or right |
| Selection checkboxes | Center |

### Managing Complexity (Scroll & Filters)
- **Horizontal Scroll:** Always fix (`position: sticky`) the first column (key identifier) and the table header.
- **Filters:** Do not show 10 empty filter fields. Use a "Filter" button that opens a Popover/Drawer. Display active filters as removable "Tags" above the table.
- **Bulk Actions:** The bulk action bar (Delete, Export) should only appear when at least one row is selected, often replacing the table header or floating at the bottom of the screen.

### Recommended CSS Structure

```css
/* Headers */
th {
  font-size: 12px;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  color: hsl(220, 10%, 55%);
  padding: 12px 16px;
  background: hsl(220, 14%, 97%);
  border-bottom: 1px solid hsl(220, 12%, 88%);
}

/* Rows */
td {
  padding: 14px 16px;
  font-size: 14px;
  border-bottom: 1px solid hsl(220, 12%, 93%);
}

/* Row Hover */
tr:hover td {
  background: hsl(220, 14%, 98%);
}
```

### Column Sorting

Indicate sorted column and its direction:
```html
<th aria-sort="ascending">
  Amount <svg class="sort-icon">↑</svg>
</th>
```

---

## Modals

### Anatomy

```
┌──────────────────────────────────┐
│ Modal Title                 [×]  │  ← Header
├──────────────────────────────────┤
│                                  │
│  Content / question              │  ← Body (scrollable if long)
│                                  │
├──────────────────────────────────┤
│ [Secondary action]  [Primary]    │  ← Footer, actions on the right
└──────────────────────────────────┘
```

**Rules:**
- One modal = one single decision or action
- Always 3 ways to close: × button, overlay click, Escape key
- Block background scroll when modal is open (`body: overflow: hidden`)
- Focus trap: keyboard navigation stays in the modal
- Strong shadow (`--shadow-xl`) to signal elevation

### Overlay

```css
.modal-overlay {
  position: fixed;
  inset: 0;
  background: rgba(0, 0, 0, 0.4);
  backdrop-filter: blur(2px);   /* optional, watch performance */
  z-index: 100;
}
```

---

## Interface States

### Empty State

Never leave a white space with just "No results". Guide the user.

```
     [Illustration or icon]
     
     You don't have any projects yet
     
     Start by creating your first project
     to organize your tasks.
     
         [Create a project]
```

**Components:**
- Illustration (optional but effective)
- Descriptive title
- Explanation message
- Main action (button)

### Loading State

| Estimated Duration | Recommended Solution |
|---|---|
| < 300ms | Nothing (fast enough) |
| 300ms – 1s | Discreet spinner |
| 1s – 3s | Skeleton screen |
| > 3s | Skeleton + status text + % if possible |

**Skeleton screen:**
```css
.skeleton {
  background: linear-gradient(
    90deg,
    hsl(220, 13%, 93%) 25%,
    hsl(220, 13%, 90%) 50%,
    hsl(220, 13%, 93%) 75%
  );
  background-size: 200% 100%;
  animation: shimmer 1.5s infinite;
  border-radius: 4px;
}

@keyframes shimmer {
  0%   { background-position: 200% 0; }
  100% { background-position: -200% 0; }
}
```

### Error State

**Structure of a good error message:**
1. What happened (without technical jargon)
2. Why it happened (if relevant)
3. How to fix it (concrete action)

```
✗ Connection failed

Your session has expired. This happens after 30 minutes of inactivity.

[Reconnect]  or  Contact support
```

**Never display:**
- `Error 500`
- `Network error: ECONNREFUSED`
- `Null pointer exception`

### Success State

```css
.toast-success {
  background: hsl(142, 70%, 96%);
  border: 1px solid hsl(142, 60%, 80%);
  color: hsl(142, 60%, 25%);
  padding: 12px 16px;
  border-radius: 8px;
  display: flex;
  align-items: center;
  gap: 10px;
}
```

---

## Notifications & Toasts

### Recommended Display Duration
- Informational toast: **3-4 seconds**
- Toast with action (Undo): **6-8 seconds**
- Error toast: **persistent until manual close**

### Position
- Desktop: bottom right corner or bottom center
- Mobile: bottom, above navigation

### Accessibility
```html
<div role="status" aria-live="polite">     <!-- for info -->
<div role="alert" aria-live="assertive">   <!-- for errors -->
```