# 08 - UI Execution Checklists

Sources: Laws of UX (Jakob, Hick, Fitts, Miller, Von Restorff, Doherty, Postel, Peak-End) - Refactoring UI - Practical UI

---

## Role of the Document

This file is not a theoretical reference. It is the control layer before production.

Objective: transform UI principles into verifiable decisions, component by component.

Application Order:
1. Respect user conventions
2. Reduce visible choices
3. Make targets easy to reach
4. Structure attention
5. Give fast and useful feedback

If two rules contradict, prioritize usability, then accessibility, then aesthetics.

Deviation authorized only if the gain is measurable: reduced task time, reduced error rate, improved conversion, improved comprehension in user testing. Without proof, go back to the conventional pattern.

---

## The 4 Fundamental Forces

UX laws are grouped into operational forces. Do not apply them one by one at random.

| Force | Main Laws | Control Question |
|---|---|---|
| Perception | Aesthetic-Usability, visual hierarchy, color | Does the interface look clear even before being read? |
| Attention | Von Restorff, Gestalt | Does the eye immediately see what matters? |
| Decision | Hick, Miller | Is the main choice obvious and limited? |
| Interaction | Fitts, Doherty, Postel | Is the action easy, fast, and tolerant? |

### Law Priority

| Level | Law | Status |
|---|---|---|
| 1 | Jakob | Mandatory Baseline: use known conventions |
| 1 | Hick | Limit visible choices before adding decoration |
| 1 | Fitts | Guarantee reachable and comfortable targets |
| 2 | Miller | Group and chunk dense information |
| 2 | Von Restorff | Highlight 1 dominant element, no more |
| 2 | Doherty | Respond quickly or show a progress state |
| 3 | Postel | Accept flexible user formats |
| 3 | Peak-End | Care for critical moments and flow ends |
| 3 | Aesthetic-Usability | Build trust through clean visual execution |

---

## Non-Negotiable Constraints

These constraints apply by default to every interface.

- 1 primary CTA maximum per view or active decision
- 5 visible choices maximum without structuring
- Unlimited choices only if grouped, filtered, hierarchical, or searchable
- 44 x 44px minimum for any touch interactive target
- Visible feedback under 300ms, otherwise spinner, skeleton, or optimistic UI
- No form field without a persistent label
- No error without understandable cause and concrete solution
- No icon-only button without an accessible name and tooltip if meaning is not universal
- No non-conventional pattern for navigation, closing, search, back, or submission
- No element highlighted if its action is not priority
- No empty state without explanation and useful next action
- Hierarchy validated in grayscale before adding color
- Minimum AA contrast on text and functional controls
- Visible focus and full keyboard navigation

---

## Global View Checklist

Before validating a page or screen:

- Main action is identifiable in less than 3 seconds
- Secondary actions are visually weaker than the main action
- Information is grouped by proximity and similarity
- Unrelated sections are separated by more space than related elements
- Visible choices are limited to useful options now
- Rare or advanced options are hidden behind progressive disclosure
- Navigation and interaction conventions are respected
- Important texts remain readable in contrast, size, and length
- 3 hierarchy levels maximum are visible simultaneously in a zone
- Fast reading follows a coherent F or Z pattern according to page type
- Body text lines remain at 80 characters maximum
- Loading, empty, error, success, and disabled states exist
- Path ends with a clear confirmation or an obvious next step

---

## Flow Control

An interface is not validated only screen by screen. The full path must remain coherent.

Checklist:
- Beginning of the flow clearly indicates objective and prerequisites
- Every transition explains what just changed
- Entered or selected data is preserved between steps
- Back buttons do not punish the user
- The end confirms the result obtained
- The next useful action is obvious after the flow ends
- Critical moments have more cared-for feedback than ordinary actions

---

## Mapping by Component

### Buttons

Dominant Laws: Fitts, Von Restorff, Hick.

Rules:
- Minimum interactive size: 44 x 44px
- 1 primary button maximum in an action group
- No equivalent double CTA
- Text = precise action verb, not "OK" or "Submit"
- Dangerous action visually separated from current action
- Frequent actions in the thumb zone on mobile
- Critical actions spatially isolated from ordinary actions
- Edges and corners used for persistent or frequent actions when context allows
- Focus, hover, active, disabled, and loading states mandatory

Checklist:
- Is the primary button the only dominant element?
- Do secondary buttons really look like secondary options?
- Is the button comfortably reachable on mobile?
- Does its position also reduce action distance, not just its size?
- Does the label announce the action result?

### Forms

Dominant Laws: Miller, Hick, Postel.

Rules:
- Mandatory persistent label for every field
- Group fields by theme
- Break into multi-step if the form exceeds 5 to 7 visible fields
- Validation on blur, except non-intrusive positive feedback
- Accept common input formats: spaces, dashes, case, prefixes
- Normalize input on the system side, not the user side
- Then display a clear canonical value
- Error message = problem + cause if useful + correction

Checklist:
- Can the field be understood without a placeholder?
- Are related fields close to each other?
- Are optional fields avoided or revealed progressively?
- Can the user go back without losing data?
- Is a common human format accepted even if it differs from the stored format?
- Does every error say how to solve it?

### Navigation

Dominant Laws: Jakob, Hick, Gestalt.

Rules:
- Use conventions: top nav, sidebar, tabs, breadcrumbs according to context
- Limit visible entries at the first level
- Group items by usage, not by company internal structure
- Clearly signal current location
- Keep global and local actions separate

Checklist:
- Can a user predict where a standard function is located?
- Are navigation items organized into obvious groups?
- Is the active level visible without dependence on color alone?
- Are rare destinations moved to "More", settings, or search?

### Dashboard

Dominant Laws: Hierarchy, Miller, Gestalt, Hick.

Rules:
- Put decision indicators before decorative data
- Limit main KPIs to 3-5
- Group data by decision to be made; data can be numerous if it remains filtered, scannable, and hierarchical
- Right-align numbers, left-align labels
- Avoid repetitive cards if a scannable table or list is more efficient
- Allow a level 2 hierarchy for secondary signals, without competing with the main signal of each zone

Checklist:
- Is the dashboard's main question obvious?
- Does important data dominate secondary data?
- Does every visualization support a concrete decision?
- Are the visible filters the most used?
- Do expert views keep a clear scan structure despite density?

### Feedback and States

Dominant Laws: Doherty, Peak-End, Aesthetic-Usability.

Rules:
- Under 300ms: not necessarily visual feedback
- 300ms to 1s: discreet spinner or local pending state
- 1s to 3s: skeleton or content structure
- Over 3s: progression, status text, or possibility to cancel
- Prefetch, cache, or pre-rendering for frequent and predictable actions
- Optimistic UI by default for non-critical and reversible actions
- Success: confirm the action and show the next step
- Error: explain without jargon and propose an action

Checklist:
- Does the user know their action was taken into account?
- Does loading preserve the expected structure?
- Can the system avoid waiting rather than just dressing it up?
- Does the flow end leave a clear and reassuring impression?
- Are errors actionable?

### Modals and Dialogs

Dominant Laws: Hick, Jakob, Fitts.

Rules:
- One modal = one decision
- Visible close button in top right
- Escape and overlay click according to risk level
- Mandatory focus trap
- Actions at the bottom, primary clearly distinguished
- Destructive action confirmed by explicit text

Checklist:
- Does the modal ask for only one thing?
- Can it be closed conventionally?
- Is the dangerous action impossible to trigger by accident?
- Does keyboard focus stay in the modal?

---

## Consolidation of Redundant Laws

Do not stack principles when they say the same thing.

| Phenomena | Associated Laws | Single Rule |
|---|---|---|
| Cognitive load | Hick + Miller | Limit unstructured choices; group, filter, or search the rest |
| Attention | Von Restorff + visual hierarchy | 1 dominant element per decision zone, with level 2 allowed |
| Organization | Gestalt + spacing | Proximity = relationship, distance = separation |
| Perceived trust | Aesthetic-Usability + color + typography | Clean execution, readable contrast, stable rhythm |
| Perceived speed | Doherty + feedback | Avoid waiting by cache/prefetch/optimistic UI; otherwise show system state |

---

## Links with Other Files

The system must be nested, not parallel.

| File | Role in the system | Executed Laws |
|---|---|---|
| `hierarchie-visuelle.md` | Prioritize what must be seen | Von Restorff, Aesthetic-Usability |
| `espacement-layout.md` | Group, separate, guide the eye | Gestalt, Miller |
| `couleur-systeme.md` | Signal status, importance, accessibility | Hierarchy, Aesthetic-Usability |
| `composants.md` | Transform principles into reusable elements | Fitts, Hick, Postel, Doherty |
| `lois-ux.md` | Theoretical reference | All, without production trade-offs |

Usage Rule:
- Read `lois-ux.md` to understand
- Use this file to decide
- Check `composants.md` to implement

---

## Quick Audit Before Delivery

Blocking:
- More than one primary CTA in the same decision
- Interactive target under 44 x 44px on touch
- Field without label
- Error without solution
- Non-conventional navigation without strong justification
- Loading over 1s without feedback
- Contrast under AA on text or functional control
- Visible focus absent
- Incomplete keyboard navigation
- Hierarchy unreadable in grayscale

Major:
- More than 5 choices visible without grouping, filter, search, or clear hierarchy
- Several visually dominant elements
- Advanced options visible by default
- Weak contrast on functional text
- Missing hover/focus/disabled/loading states
- Flow without clear beginning, explicit transition, or exploitable end
- Dense interface without clear scan path

Minor:
- Vague microcopy
- Inconsistent spacing between groups
- Flat or uninformative flow end
- Decorative animation without function
- Body text lines too long

Decision:
- Every blocking issue must be corrected before delivery
- Major issues must be corrected or explicitly accepted
- Minor issues can enter a polish pass
