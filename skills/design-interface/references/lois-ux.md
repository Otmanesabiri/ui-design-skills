# 06 — UX Laws (Applied Psychology)

Source: Laws of UX 2nd ed. — Jon Yablonski

---

## Overview

| Law | Principle in one sentence | Main Impact |
|-----|----------------------|-----------------|
| Jakob's Law | Users prefer what looks like what they already know | Navigation, patterns |
| Fitts's Law | The larger and closer it is, the easier it is to reach | Size and position of targets |
| Miller's Law | Working memory is limited to ~7 elements | Grouping, progressive disclosure |
| Hick's Law | The more choices, the slower the decision | Simplification of options |
| Postel's Law | Be strict in what you produce, flexible in what you accept | Robustness, accessibility |
| Peak-End Rule | We judge an experience by its peak and its end | Onboarding, confirmation, error |
| Aesthetic-Usability Effect | Beautiful interfaces seem easier | Visual quality and trust |
| Von Restorff Effect | What differs is remembered | Highlighting key elements |
| Tesler's Law | Complexity is incompressible, it moves | UX simplification vs backend complexity |
| Doherty Threshold | Max productivity under 400ms latency | Perceived performance, feedback |

---

## 1. Jakob's Law

> "Users spend most of their time on other sites. They prefer your site to work like all the others they already know."
>
> — Jakob Nielsen, 2000

### Principle
Users build mental models of how interfaces work from their accumulated experience. When a new interface respects these models, the learning curve is nearly zero.

### Concrete Applications
- Logo in top left → clickable to home
- Main navigation at the top or left
- Close button (×) in top right of modals
- Search field with magnifying glass icon
- Breadcrumbs for hierarchical navigation
- Cart icon for e-commerce

### When to Innovate
Innovate on **content**, not on **interaction patterns**. Breaking with conventions costs the user cognitive energy. This cost must be justified by real value.

### Common Error
Creating unconventional navigation to differentiate. The user wants to accomplish a task, not learn a new navigation.

---

## 2. Fitts's Law

> "The time to acquire a target is a function of the distance to and size of the target."
>
> — Paul Fitts, 1954

### Simplified Formula
The **larger** and **closer** the target is to the starting point, the less time it takes to reach it.

### Concrete Applications

**Touch target size (mobile)**
Recommended minimum size: **44 × 44px** (Apple HIG, WCAG 2.5.5 level AAA: 44×44px, level AA: 24×24px)
```css
.btn {
  min-width: 44px;
  min-height: 44px;
}
```

**Frequent actions → bottom of the screen on mobile**
The natural thumb zone is at the bottom of the screen. Primary actions (CTA, tab bar) should be there.

**Avoid dangerous actions near common actions**
Do not place "Delete" next to "Save" without sufficient space.

**Edges and corners of screen**
Edges and corners of the screen are "infinitely large targets" (the cursor stops there naturally). macOS menus at the top of the screen exploit this.

### Common Error
Putting "Accept" and "Refuse" side by side in small size in a dialog. The user must lift their thumb or zoom to select the right button.

---

## 3. Miller's Law

> "The average person can keep 7 (±2) items in working memory."
>
> — George Miller, 1956

### What this law does NOT say
Miller's Law does **not** say that navigation must be limited to 7 items. Using this number as a strict limit is a poor application of the law.

### What it really says
Working memory is limited. Too many or too dense pieces of information create cognitive overload.

### Concrete Applications
- **Chunking**: grouping information into logical blocks (e.g., phone numbers `06 12 34 56 78` and not `0612345678`)
- **Progressive disclosure**: revealing information gradually
- **Multi-step forms**: breaking up long forms

### Real size of working memory
More recent research (Cowan, 2001) suggests **4 items** as a limit. Miller's Law is less precise than believed.

---

## 4. Hick's Law

> "Decision-making time increases with the number and complexity of available choices."
>
> — Hick & Hyman, 1952

### Formula
`T = b × log₂(n + 1)` — decision time is logarithmic, not linear.

### Concrete Applications

**Reduce visible options**
Netflix found users took an average of 18 minutes to choose what to watch. Solution: "Trending Now", "Popular on Netflix" — reduce perceived choice field.

**Progressive disclosure**
Show advanced options only when the user explicitly asks for them.
```
[Basic options visible]
+ Show advanced options ↓
```

**Progressive onboarding**
Do not present all features at first launch. Introduce features when the user needs them.
Duolingo example: unlock "Legendary Levels" only after completing a normal level.

**Recommendations**
Proposing a default or recommended option reduces decision load.
```
○ Monthly — 9.99€/month
● Yearly — 7.99€/month  ← Recommended (save 24%)
○ Lifetime — 199€
```

### Common Error
Displaying 12 options in a dropdown when 4-5 cover 90% of cases. Add "Other options..." for rare cases.

---

## 5. Postel's Law (Robustness Principle)

> "Be conservative in what you do, be liberal in what you accept from others."
>
> — Jon Postel (RFC 793, 1981)

### Principle
The interface must be robust and adapt to the user, not the other way around.

### Concrete Applications

**Flexible inputs**
```
Phone accepted in all forms:
0612345678
06 12 34 56 78
+33 6 12 34 56 78
06-12-34-56-78
```

**Flexible capitalization**
Email fields should accept `JOHN@EXAMPLE.COM` and `john@example.com` indifferently.

**Responsive design**
Adapt to all screen sizes, resolutions, and pixel densities.

**Font size customization**
Amazon adapts its navigation when the user increases system font size: less important links disappear to make room.

**Input methods**
Accept keyboard, mouse, touch, and assistive technologies (screen readers, switches).

### Common Error
Rejecting a phone number because it contains spaces or dashes. Formatting is the interface's responsibility, not the user's.

---

## 6. Peak-End Rule

> "People judge an experience primarily by its emotional peak and its end, not by the average."
>
> — Kahneman & Fredrickson, 1993

### Principle
Memory of an experience is not the sum of all its moments. It is dominated by:
1. The **most intense moment** (positive or negative)
2. The **end** of the experience

### Concrete Applications

**Care for the end of flows**
- Payment confirmation → warm message, clear summary, obvious next step
- Completed signup → visual celebration, not a blank page
- Account deletion → understanding message, recovery option

**Create positive peaks**
- Success animation after an important action
- Personalized message after onboarding
- Easter egg or surprise micro-interaction

**Mitigate negative peaks**
- Human and actionable error message (not "Error 500")
- Useful 404 page with suggestions
- Loading state with partial content (skeleton) rather than a blank spinner

**Duolingo**
The "streak" (number of consecutive days) is a strong emotional peak. Losing your streak is a negative peak remembered for a long time — creating engagement through loss aversion.

---

## 7. Aesthetic-Usability Effect

> "Visually attractive interfaces are perceived as easier to use."
>
> — Kurosu & Kashimura, 1995 (Hitachi Design Center)

### Original Study
26 ATM layouts tested with 252 participants. Visually attractive designs were perceived as easier to use, regardless of their real usability.

### Implications
- A beautiful design increases tolerance for minor errors and bugs
- An attractive design generates more initial trust
- Users are more forgiving of problems if they like the interface

### Caution
This effect can mask real usability problems. Users do not always identify problems of an attractive design. This makes user testing all the more important.

---

## 8. Von Restorff Effect (Isolation Effect)

> "Among several similar objects, the one that differs from the others is most likely to be remembered."
>
> — Hedwig von Restorff, 1933

### Concrete Applications
- "New" or "Popular" badge on a pricing option
- CTA button of a color that breaks with the rest of the interface
- Highlighted element in a list (colored background, distinctive icon)

### Critical Rule: Do Not Over-use
If everything is highlighted, nothing is. Reserve differentiation for **1 or 2 elements maximum** per view.

```
✗ Bad: 3 differently colored buttons + 2 "New" badges
✓ Good: 1 clearly distinct primary button + 1 "Recommended" badge
```

---

## 9. Tesler's Law (Conservation of Complexity)

> "For any system, there is a certain amount of complexity that cannot be reduced."
>
> — Larry Tesler

### Principle
Complexity does not disappear — it moves. If the interface is simplified, complexity is transferred to the developer or backend system.

### Concrete Applications

**Good example: address form**
Simple option (user): enter the full address in free text
Complex option (developer): parse, validate, and normalize the address
→ Transferring complexity to the system (address autocompletion) is the right choice here.

**Bad example: code editor**
Hiding syntax to "simplify" a code editor transfers complexity to the user who no longer understands what is happening.
→ Sometimes complexity must remain visible to the user.

### Active User Paradox
Users start using software **immediately** without reading documentation. They prefer to accomplish a task now rather than learn the system first. Design taking this behavior into account.

---

## 10. Doherty Threshold

> "Productivity increases significantly when system and user interact at less than 400ms."
>
> — Walter Doherty & Ahrvind Thadani, 1982

### Perception Thresholds
| Delay | Perception | Behavior |
|-------|-----------|-------------|
| < 100ms | Instantaneous | Feeling of total responsiveness |
| 100–300ms | Near-instantaneous | Acceptable, no feedback needed |
| 300–1000ms | Perceptible | Minimal loading indicator recommended |
| 1–10s | Waiting | Progress bar or skeleton necessary |
| > 10s | Probable abandonment | Detailed feedback + cancellation option |

### Concrete Applications

**Optimistic UI**
Update the interface immediately (before server response) and rollback on error. The user perceives total responsiveness.

**Skeleton screens**
Show the page structure (gray, element shapes) before content loads. Reduces perception of waiting.

**Gmail loading animation**
Use a simple logo animation + progress bar. Creates the perception of a shorter load.

**Animated progress bars**
Progress bars that animate slightly seem to progress faster. Animation compensates for perception of slowness.

---

## Gestalt Principles (Foundation of Visual Organization)

While not "laws of UX" in the strict sense, they underlie all visual laws.

| Principle | Description | UI Usage |
|----------|-------------|---------|
| **Proximity** | Close elements seem related | Group form elements |
| **Similarity** | Similar elements seem related | Same style for items of the same type |
| **Continuity** | The eye follows a line or curve | Alignments, horizontal scroll rails |
| **Closure** | The mind completes incomplete shapes | Minimalist icons, partial borders |
| **Common Region** | Elements in a container seem related | Cards, form groups |
| **Figure-Ground** | Distinguish main object from background | Modals with overlay, tooltips |

---

## Ethics and Responsibility

> "With great power comes great responsibility."

### Dark Patterns to Identify and Avoid

| Pattern | Description | Example |
|---------|-------------|---------|
| **Confirmshaming** | Naming refusal in a shaming way | "No thanks, I prefer paying more" |
| **Hidden costs** | Revealing fees only at the final step | Service fees at checkout |
| **Roach motel** | Easy to enter, hard to exit | Easy signup, laborious cancellation |
| **Misdirection** | Drawing attention away from what matters | Disabled button vs recommended option |
| **Disguised ads** | Ads imitating content | Indistinguishable "sponsored article" |
| **Trick questions** | Forms with misleading pre-checks | Newsletter checked by default |

### The Line Between Persuasion and Manipulation
- **Persuasion**: presenting real value of a product, facilitating good decisions
- **Manipulation**: exploiting cognitive biases to obtain actions the user would regret

The rule: ethical design improves user experience **and** serves business objectives. Not one at the expense of the other.