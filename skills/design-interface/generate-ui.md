# Generate UI - Creation Procedure

Objective: produce a usable interface from the first screen, consistent with the skill references, without starting with a marketing page or unnecessary decoration.

References to use:
- `references/processus-decisions.md` to frame the feature
- `references/checklists.md` for executable constraints
- `references/hierarchie-visuelle.md` to prioritize content
- `references/espacement-layout.md` to organize the page
- `references/couleur-systeme.md` and `references/tokens.md` for visual values
- `references/composants.md` for expected components
- `references/antipatterns-ethique.md` for guardrails

---

## 1. Frame Before Drawing

Do not start with "making a beautiful page". Start with the user task.

Mandatory Questions:
- Who uses this interface?
- What main action must be accomplished?
- What information is necessary before this action?
- What information can be hidden, deferred, or calculated?
- What is the main risk: confusion, error, slowness, lack of trust?

Expected Output:
- 1 main objective
- 1 primary CTA
- 3 to 5 pieces of information or actions visible by priority
- Necessary states: loading, empty, error, success, disabled

---

## 2. Build the Structure

Construction order:
1. Content and data
2. Hierarchy
3. Layout
4. Components
5. Color
6. Micro-interactions

Rules:
- Design in grayscale mentally first: color should not carry hierarchy alone
- 1 dominant element per decision zone
- 3 visible hierarchy levels maximum in a zone
- Related elements are close; distinct groups are clearly separated
- Lines of body text remain at 80 characters maximum

---

## 3. Choose the Layout According to the Product

### SaaS, CRM, admin, dashboard

Priority: readable density, fast scanning, predictable actions.

Recommended Patterns:
- Sidebar or conventional top nav
- Compact header with title, context, and actions
- Scannable tables or lists for repetitive data
- Filters visible only if frequent
- Panels, drawers, or detail pages for secondary complexity

Avoid:
- Marketing hero
- Large decorative cards for tabular data
- Illustrations replacing useful controls
- Color used as the only signal

### Consumer App

Priority: simple path, clear decision, reassuring feedback.

Recommended Patterns:
- Familiar navigation
- Visible primary CTA
- Progressive disclosure
- Useful empty states
- Clear confirmation at the end of the flow

### Landing Page or Brand Page

Priority: immediate understanding of the offer.

Recommended Patterns:
- Product, place, service, or object must be visible from the first viewport
- H1 = concrete name, offer, or category
- Real image or relevant visual scene
- A hint of the next section remains visible
- Single main CTA

---

## 4. Apply Non-Negotiable Constraints

Before implementing:
- 1 primary CTA maximum per active decision
- 5 visible choices maximum without structuring
- Many choices allowed if grouped, filtered, hierarchical, or searchable
- 44 x 44px minimum for touch target
- Feedback under 300ms or progress state
- No field without a persistent label
- No error without a solution
- Visible focus and full keyboard navigation
- Minimum AA contrast on text and functional controls
- Hierarchy readable in grayscale

---

## 5. Compose Components

### Buttons

- Text with precise action verb
- Primary = main action only
- Secondary = useful but less important alternative
- Tertiary = secondary action, link, or discreet text
- Dangerous actions spatially separated
- Loading state preserves button width if possible

### Forms

- Persistent labels above fields
- Fields grouped by theme
- Multi-step if the form becomes dense
- Validation on blur
- Flexible formats accepted then normalized
- Actionable errors under the field concerned

### Navigation

- Respect conventions of the product type
- Active item visible without dependence on color alone
- Group by user usage
- Put rare destinations in search, settings, or "More"

### Dashboard

- Main KPIs limited to 3-5
- Many data allowed if scannable
- Useful filters at the top or near the data concerned
- Numbers right-aligned
- Statuses accompanied by text or icon, not color alone

---

## 6. Manage States

Every generated interface must provide:

| State | Requirement |
|---|---|
| Loading | Local spinner, skeleton, or optimistic UI depending on duration |
| Empty | Useful message + next action |
| Error | Clear cause + solution |
| Success | Confirmation + next step |
| Disabled | Explicit reason if action is expected |
| Focus | Visible indicator for keyboard |

Doherty Rule:
- Avoid waiting with cache, prefetch, pre-rendering, or optimistic UI
- If waiting remains visible, show the system state

---

## 7. Verify Before Delivery

Final Checklist:
- Screen objective is clear in less than 3 seconds
- Primary CTA is unique
- Numerous choices are structured
- Hierarchy works without color
- Touch sizes respect 44 x 44px
- Flow transitions are explicit
- Errors do not blame the user
- Design uses no dark patterns
- Interface remains readable on mobile and desktop
- No text overflows its container

Expected Result: a functional, scannable, accessible, and directly exploitable UI.
