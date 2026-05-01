# Improve UI - Improvement Procedure

Objective: improve an existing interface without reinventing it unnecessarily. Priority to problems that block understanding, action, accessibility, or trust.

References to use:
- `references/checklists.md` to classify problems
- `references/hierarchie-visuelle.md` to correct prioritization
- `references/espacement-layout.md` to clarify groups
- `references/couleur-systeme.md` for contrast and signals
- `references/composants.md` for states and patterns
- `references/antipatterns-ethique.md` to avoid manipulation

---

## 1. Diagnose Before Modifying

Read the interface like a rushed user.

Questions:
- What should I do here?
- Which action is most important?
- What is secondary?
- Where can I go wrong?
- What looks clickable but isn't?
- What is clickable but doesn't look it?

Classify problems:
- Blocking: prevents usage, accessibility, or decision
- Major: slows down, confuses, or increases error risk
- Minor: polish, consistency, comfort

---

## 2. Order of Correction

Do not start with color.

1. Clarify the objective of the view
2. Reduce or structure choices
3. Repair visual hierarchy
4. Correct spacing and groups
5. Correct components and their states
6. Correct accessibility and keyboard
7. Add visual polish

Rule: if a correction is only aesthetic but does not solve any comprehension or usage problem, postpone it.

---

## 3. Frequent Corrections

### Too Much Visual Noise

Symptoms:
- Several buttons seem primary
- Too many badges, colors, or shadows
- Titles, cards, and actions have the same weight

Corrections:
- Keep 1 dominant element per decision zone
- De-emphasize secondary actions
- Reduce decorative shadows and backgrounds
- Test the page in grayscale

### Too Many Choices

Symptoms:
- Long lists of visible actions
- Filters and advanced options always open
- User must read before knowing what to do

Corrections:
- Keep 3-5 unstructured choices visible
- Group, filter, or search numerous choices
- Put rare options behind "More" or "Advanced"
- Propose a recommended option if useful

### Hard-to-Fill Form

Symptoms:
- Placeholders used as labels
- Late or vague errors
- Too strict imposed format
- Optional fields everywhere

Corrections:
- Persistent labels
- Grouping by theme
- Validation on blur
- Flexible formats then canonical display
- Error = problem + solution
- Optional fields revealed progressively

### Heavy Dashboard

Symptoms:
- Too many identical cards
- KPIs without associated decision
- Unreadable table
- Too many filters

Corrections:
- Limit main KPIs to 3-5
- Transform repetitive cards into table or list
- Right-align numbers
- Add sort, filter, search if volume is high
- Keep a clear scan path

### Weak Feedback

Symptoms:
- Nothing happens after click
- Global loading for a local action
- Raw technical error
- Success without next step

Corrections:
- Local feedback under 300ms
- Optimistic UI for reversible actions
- Skeleton for structured content
- Human and actionable messages
- End of flow with result + next action

---

## 4. Intervention Rules

Do:
- Conserve existing patterns when they work
- Correct by small, verifiable passes
- Use existing tokens before creating new ones
- Reinforce hierarchy by size, weight, spacing, and contrast
- Check mobile and desktop

Avoid:
- Adding a new palette to mask a structural problem
- Replacing all cards with other cards
- Adding an animation without a function
- Using color alone to signal a state
- Breaking a convention without measurable gain

---

## 5. Before/After Checklist

Before finishing:
- Is the initial problem resolved?
- Is the main action more obvious?
- Has the number of unstructured choices decreased?
- Are related zones better grouped?
- Are contrasts and focus compliant?
- Do loading, error, empty, and success states exist?
- Does density remain scannable?
- Has no dark pattern been introduced?

Expected Deliverable:
- Short list of changes
- Why each change improves usage
- Remaining risks or points to test
