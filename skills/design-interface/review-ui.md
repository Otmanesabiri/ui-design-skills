# Review UI - Audit Procedure

Objective: evaluate an interface with a review posture. Problems come before compliments. Findings must be actionable, classified by severity, and linked to user impact.

References to use:
- `references/checklists.md` for blocking and major issues
- `references/lois-ux.md` to explain the principle if necessary
- `references/composants.md` to verify patterns
- `references/couleur-systeme.md` for color accessibility
- `references/antipatterns-ethique.md` for manipulation risks

---

## Recommended Output Format

1. Critical and major findings
2. Open questions or hypotheses
3. Useful positive points
4. Short summary

Each finding must contain:
- Severity: blocking, major, minor
- Location: screen, zone, component, or file if available
- Observed problem
- User impact
- Recommended correction

Avoid vague opinions: "it's pretty", "it's modern", "to be improved".

---

## Severity Grid

### Blocking

Problem that prevents or strongly compromises usage:
- Main CTA absent or competing with another primary CTA
- Field without label
- Error without solution
- Contrast under AA on functional text
- Visible focus absent
- Incomplete keyboard navigation
- Touch target under 44 x 44px
- Dangerous action too easy to trigger
- Manifest dark pattern

### Major

Problem that slows down, confuses, or increases errors:
- More than 5 visible choices without structuring
- Hierarchy unreadable in grayscale
- Too many dominant elements in a zone
- Advanced options visible by default
- Long loading without feedback structure
- Flow without clear beginning, explicit transition, or useful end
- Dense dashboard without scan possible
- Color used as the only signal

### Minor

Problem of polish or consistency:
- Vague microcopy
- Inconsistent spacing
- Text lines too long
- Animation without function
- Inconsistent radius, shadows, or paddings
- Unengaging empty state but not blocking

---

## Audit Checklist

### Objective and Decision

- Is the view objective clear in less than 3 seconds?
- Is the main action unique?
- Are secondary actions visually secondary?
- Are numerous choices grouped, filtered, hierarchical, or searchable?
- Is there a recommended option when the choice is complex?

### Hierarchy and Scan

- Does the page work in grayscale?
- Are 3 hierarchy levels maximum visible in a zone?
- Does quick reading follow a coherent F or Z pattern?
- Do titles, labels, values, and actions have distinct weights?
- Does important data dominate decorative data?

### Layout and Spacing

- Are related elements close?
- Do distinct groups have enough space?
- Do alignments facilitate comparison?
- Are cards useful or do they replace a more efficient table?
- Is density adapted to the product type?

### Components

- Buttons: correct sizes, states, labels, and hierarchy?
- Forms: persistent labels, validation on blur, actionable errors?
- Navigation: conventional, grouped, clear active state?
- Tables: correct alignment, sort, status, actions, and empty state?
- Modals: one decision, clear closing, focus trap?

### Feedback and Flow

- Does the interface respond under 300ms or explain the wait?
- Are cache, prefetch, or optimistic UI possible?
- Are flow transitions explicit?
- Does the end of the path confirm the result?
- Is the next action obvious?

### Accessibility

- Minimum AA contrast?
- Visible focus?
- Full keyboard navigation?
- Accessible labels and names?
- Color backed by text, icon, or shape?
- Text readable and not truncated?

### Ethics

- Can the user refuse as easily as accept?
- Are costs, consequences, and commitments visible before action?
- Are options formulated without shaming?
- Do defaults serve the user as much as the business?
- Is exiting a subscription, account, or flow accessible?

---

## Immediate Red Flags

Stop the review and signal strongly if:
- Primary button used for a misleading action
- Refusal hidden, weakened, or shaming
- Fees revealed late
- Unsubscribing harder than signing up
- Pre-checked consent
- Destructive data without clear confirmation
- Interface unusable with keyboard

---

## Finding Example

Blocking - Payment Form

The "Zip Code" field has no persistent label and only uses a placeholder. As soon as the user enters a value, the meaning of the field disappears, which increases the risk of error and poses an accessibility problem. Add a visible label above the field and keep the placeholder only as a format example.

---

## Final Decision

Use this conclusion:
- Ready: no blocking, major issues accepted or corrected
- Ready with reservations: no blocking, some major issues documented
- Not ready: at least one blocking issue or major ethical risk
