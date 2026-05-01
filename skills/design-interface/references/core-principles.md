# Core UI Principles (Context Optimization)

**Agent Instruction:** This is the MASTER file. Read this file first for any UI design or review task. It contains the 10 absolute golden rules. ONLY load other specific reference files if this summary is insufficient for the task, or if exact mathematical formulas/tokens are requested.

---

## 1. Feature First, Layout Second
Never start by designing a navigation bar. Identify the core user task, the necessary data, and the primary action. The layout must serve the feature, not the other way around.

## 2. Grayscale Before Color (Hierarchy)
Design in black and white first. Use **size, weight, spacing, and contrast** as your only hierarchy levers. If the hierarchy fails in grayscale, color will not fix it.

## 3. One Decision = One Primary Action
Never place two primary buttons (solid background) side by side. For every section or modal, there is only ONE primary action. The rest must be secondary (outline) or tertiary (text link).

## 4. Spacing > Borders
To group or separate elements, use spacing (proximity) first. Only use borders or backgrounds if spacing alone is insufficient. Do not trap every element inside a box.

## 5. Systemic Values Only
Never invent arbitrary pixel values. 
- Use a 4px/8px based spacing scale (e.g., 4, 8, 16, 24, 32).
- Use a predefined typographic scale (e.g., 14, 16, 20, 24, 30).
- Use a predefined color palette with 9 shades (100 to 900).

## 6. Color is Not Enough (Accessibility)
Never use color as the sole indicator of state (error, success). Always back it up with an icon, text, or a specific shape. Contrast must meet WCAG AA (4.5:1 for normal text, 3:1 for large text).

## 7. Reduce Cognitive Load (Hick's & Miller's Laws)
If a view has more than 5 choices, structure them. Hide advanced options behind progressive disclosure ("More..."). Chunk dense data into scannable blocks.

## 8. Accessible Targets (Fitts's Law)
Any interactive element designed for touch must have a minimum size of 44x44px. This includes text fields, buttons, and icons.

## 9. Immediate Feedback (Doherty Threshold)
The system must react in less than 400ms. If an action takes longer, show a skeleton, a spinner, or use Optimistic UI. Never leave the user wondering if their click registered.

## 10. Ethical Design
No dark patterns. Costs must be visible before action. Unsubscribing must be as easy as subscribing. Do not shame the user for refusing an offer (Confirmshaming). The interface must serve both the business AND the user.
