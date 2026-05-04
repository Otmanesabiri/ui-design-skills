# Core UI Principles (Context Optimization)

**Agent Instruction:** MASTER file. Read FIRST. Covers 90% of tasks. Load specialized refs ONLY for exact math/tokens.

---

## 1. Feature > Layout
`Rule[Process]: Feature_First. Forbid(Nav_First, Shell_First).`
Map core tasks + data + primary action before designing containers.

## 2. Grayscale Hierarchy
`Rule[Hierarchy]: Grayscale_First. Levers(Size, Weight, Spacing, Contrast).`
If B&W hierarchy fails, color is invalid.

## 3. Atomic Decisions
`Rule[Action]: Single_Primary_Per_View. Hierarchy(Primary > Secondary > Tertiary).`
Never side-by-side solid buttons. 1 modal = 1 goal.

## 4. Proximity > Containers
`Rule[Grouping]: Spacing_First. Forbid(Box_Trapping).`
Use whitespace for separation. Borders/BG = Last resort.

## 5. Systemic Constraints
`Rule[Values]: Strict_Scale_Only. Spacing(4/8px). Type(Scale_Ref). Color(100-900).`
Zero arbitrary pixels. Values must exist in `tokens.md`.

## 6. Multi-Modal Feedback
`Rule[A11y]: Color_!=_Signal. Requirement(Icon|Text|Shape). Verify(Contrast_AA_4.5:1).`
Color must not be the unique state indicator.

## 7. Cognitive Shield
`Rule[UX]: Chunking(Max_5_Choices). Technique(Progressive_Disclosure).`
Scannable blocks for dense data. Hide "Advanced" by default.

## 8. Physical Accuracy (Fitts)
`Rule[Touch]: Min_Target(44x44px). Scope(Input, Button, Icon).`
Account for thumb zone and finger size.

## 9. Temporal Response (Doherty)
`Rule[Performance]: Response_Threshold(<400ms). Latency_UI(Skeleton|Spinner|Optimistic).`
Zero ambiguity on action registration.

## 10. Ethical Framework
`Rule[Ethics]: Anti_Dark_Patterns. Forbid(Confirmshaming, Hidden_Costs).`
Equality: Subscribing_Ease == Unsubscribing_Ease.

