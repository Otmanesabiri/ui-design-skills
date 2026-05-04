# UI Components (Context Optimization)

**Agent Instruction:** Use for component-specific design. For CSS values, reference `tokens.md`. For UX logic, see `lois-ux.md`.

---

## Buttons
`Component[Button]: { display: inline-flex, align: center, gap: 8px, h: 44px_min, radius: var(--radius-md) }`
`Text: { weight: 600, size: 14px, case: sentence, action: "Verb + Object" }`

### States & Sizes
| State | Behavior | Size | Spec (Padding | Font) |
|---|---|---|---|
| Default | brand.500, shadow.sm | xs | 4/10 | 12px |
| Hover | color-100, shadow.md | sm | 6/14 | 13px |
| Focus | 2px.outline + 2px.offset | **md** | **10/20** | **14px** |
| Active | color-200, shadow.none | lg | 14/28 | 16px |
| Disabled | opacity.0.5, cursor.not-allowed | xl | 18/36 | 18px |

---

## Forms
`Structure: Title -> Grouped_Fields -> Helper_Text -> Inline_Validation -> Primary_Action(Bottom_Right).`

### Inputs & Labels
`Label: { display: block, size: 14px, weight: 500, pos: top }`
`Input: { size: 16px_min(iOS), border: 1.5px, radius: var(--radius-md), transition: 150ms }`
`States: Focus(outline:none, border:brand.500, shadow:glow), Error(border:error.500), Disabled(bg:gray.100, opacity:0.7).`

### Validation Logic
`Timing: On_Blur ( Keystroke = ❌, Success_Icon = ✓ ).`
`MultiStep: { progress: "Step X of Y", logic: group_related, forbid: premature_save }.`
`Optional: Forbid(label_optional). Prefer(Progressive_Opt_In).`

### Mobile Optimizations
`Tel: { type: tel, autocomplete: tel, inputmode: tel }`
`Email: { type: email, autocomplete: email, inputmode: email }`
`Numeric: { type: text, inputmode: numeric, pattern: "[0-9]*" }`

---

## Data Tables
`Apply: Miller's_Law (Chunking). Forbid(Dense_1_Column_Per_Data).`
`Merge: { avatar + name + email } -> 1 User Cell.`

### Alignment Rules
| Data Type | Align | Logic |
|---|---|---|
| Text / Users | Left | Natural reading |
| Numbers / Amounts | **Right** | Column comparison |
| Status / Icons | Center | Visual balance |

### Complex Data Logic
- `Sticky: Header + 1st_Column (Identifier).`
- `Filters: Forbid(10_empty_fields). Use(Popover_Filter + Active_Tags).`
- `Bulk: Show(Batch_Action_Bar) ONLY on row_selection.`

---

## Modals & Overlays
`Anatomy: Header(Title + X) -> Body(Scrollable) -> Footer(Primary_Right).`
`Logic: Close(X_Btn | Overlay_Click | Esc). Forbid(Body_Scroll).`
`Overlay: { pos: fixed, bg: rgba(0,0,0,0.4), blur: 2px, z: 100 }.`

---

## Interface States

### Empty State
`Requirement: Icon -> Title -> Context -> Primary_CTA.`
`Goal: Guide user, do not just inform of absence.`

### Loading (Doherty)
- `< 300ms`: None.
- `300ms-1s`: Spinner.
- `1s-3s`: **Skeleton** (shimmer, match final shape).
- `> 3s`: Skeleton + Status text.

### Error Messages
`Structure: WHAT_happened -> WHY_happened -> HOW_to_fix.`
`Forbid: Tech_Jargon (Error 500, ECONNREFUSED).`

### Toasts & Notifications
`Duration: Info(3-4s), Undo(6-8s), Error(Persistent).`
`A11y: role="status" (Info), role="alert" (Error).`