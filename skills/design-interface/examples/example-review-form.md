# Example: Form Review

**User Request:** "Can you review my payment form? It looks a bit messy."

## Agent Response (Based on UI Skills)

### Blocking Issues 🔴
- **Competing Buttons:** The "Cancel" and "Pay" buttons have the same visual weight (both with a solid background). **Fix:** The "Pay" button should be the primary button (`var(--color-brand)`), and "Cancel" should be secondary (text only or simple outline).
- **Fitts's Law:** Text fields and buttons are too small (32px height). **Fix:** Increase the minimum height to `44px` to facilitate clicks, especially on mobile.

### Major Improvements 🟡
- **Logical Grouping (Chunking):** Credit card information and billing address are mixed. **Fix:** Separate into two distinct sections with clear titles ("Payment Information" and "Billing Address") with a `margin-bottom` of `32px` (`var(--space-8)`) between sections.
- **Labels and Placeholders:** Using placeholders instead of real labels above fields hurts accessibility if the user forgets what they were filling out. **Fix:** Place clear labels above each field with a tight `var(--space-1)` (4px) spacing.

### Minor Improvements 🟢
- **Border Color:** Field borders use a black that is too harsh (`#000000`). **Fix:** Use `var(--color-border-normal)` to soften the visual rendering.
- **Visual Feedback (Focus):** The state when clicking on a field (focus) lacks a clear indication. **Fix:** Add an outline in the primary color (`var(--color-brand)`) during `focus` to clearly indicate where the user is.

### Proposed Result
```css
/* Applying new tokens for the form */
.form-section {
  margin-bottom: var(--space-8); /* 32px */
}
.form-label {
  display: block;
  font-size: var(--text-sm);
  font-weight: 500;
  color: var(--color-text-primary);
  margin-bottom: var(--space-1); /* 4px */
}
.form-input {
  min-height: 44px; /* Accessible touch target */
  padding: var(--space-3);
  border: 1px solid var(--color-border-normal);
  border-radius: var(--radius-md);
  width: 100%;
}
.form-input:focus {
  outline: 2px solid var(--color-brand);
  border-color: transparent;
}
.btn-primary {
  background-color: var(--color-brand);
  color: var(--color-text-inverse);
  min-height: 44px;
  /* ... */
}
.btn-secondary {
  background-color: transparent;
  color: var(--color-text-secondary);
  /* ... */
}
```

### Expected Result 👁️
The form will be transformed into a structured view: two well-separated distinct blocks (card info, address). Fields will have readable labels above, and a generous height of 44px making input comfortable. Action buttons will be obvious: the "Pay" button will stand out massively thanks to its brand color (`--color-brand`), while the "Cancel" button will be discreet. Saising will be accompanied by a clear outline on focus, improving overall accessibility.
