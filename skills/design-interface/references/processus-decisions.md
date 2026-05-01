# 01 — Design Process & Decisions

Sources: Refactoring UI ch.1 · Practical UI ch.1 (Fundamentals)

---

## Where to Start

### Fundamental Rule: Feature First, Layout Second
Never start with "design the app". Start with a concrete and functional feature.

**Bad Approach:**
- Where does the navigation go?
- Top nav or sidebar?
- Where do we put the logo?

These questions are premature. Without having designed some features, you don't have the information to answer them.

**Good Approach:**
Choose the first feature to design (e.g., "search for a flight") and list only what it needs:
- Departure city field
- Arrival city field
- Departure date field
- Return date field
- Search button

Start with that. The layout emerges naturally afterwards.

---

## Working in Low Fidelity

### Why
In the early stages, focusing on fonts, shadows, and colors is a waste of time. These decisions depend on content and structure — which aren't defined yet.

### How
- Draw on paper with a thick Sharpie — impossible to focus on details
- Design in grayscale in the design tool — forces the use of spacing, contrast, and size as the only levers of hierarchy
- Wireframes are **disposable** — do not over-invest in them

### Benefit of Grayscale
In grayscale, you are forced to use:
- Spacing to create separation
- Contrast to create importance
- Size to signal hierarchy

Result: an interface with strong and clear hierarchy, easy to enrich with color afterwards.

---

## Don't Over-design

### Don't Plan for Hypothetical Features
Design only what users need today. Hypothetical features ("what if the user wants to do X?") clutter the interface without proven value.

### Iterate Quickly
Static mockups have no value for users. Use them to explore ideas, then leave them behind as soon as a direction is validated. Move to real implementation as quickly as possible.

---

## Choose a Personality

Before choosing colors and fonts, define the interface's personality. Personality dictates aesthetic choices.

### Personality Axes

| Personality | Typography | Color | Border-radius |
|---|---|---|---|
| Elegant / Classic | Serif | Gold, Black, White | Small (2-4px) |
| Neutral / Professional | Neutral Sans-serif | Blue, Gray | Medium (4-8px) |
| Playful / Accessible | Rounded Sans-serif | Bright colors | Large (8-16px+) |
| Secure / Institutional | Readable Sans-serif | Blue, Green | Medium |

### Color and Psychology
- **Blue**: safe, familiar, universal — no one complains about blue
- **Gold / Dark Yellow**: premium, sophisticated, luxury
- **Pink**: light, casual, not serious
- **Green**: nature, health, success, growth
- **Red**: danger, urgency, energy
- **Purple**: creativity, spirituality, mystery

---

## Limit Choices

### The Problem of Total Freedom
When you have too many options, you waste time deciding. The solution is to define systems in advance that constrain choices to a reasonable set.

### Systems to Define Upfront
1. **Color Palette** — 8-10 shades per color, defined once
2. **Typographic Scale** — 8-10 fixed sizes
3. **Spacing System** — predefined values (4/8/16/24/32…)
4. **Shadow Scale** — 5 elevation levels
5. **Border-radius** — 2-3 fixed values

Once these systems are defined, every decision comes down to "which system value to use?" rather than "what value to invent?".

---

## Have a Logical Reason for Every Detail

### Fundamental Principle (Practical UI)
UI design importance is often reduced to "making it pretty". This is a mistake. If an interface is well-designed, **every detail has a logical reason that improves usability**.

Some elements are purely decorative, but even they must have a justification: creating depth, guiding the eye, signaling a hierarchy.

### Question to Ask for Every Element
> "Why is this element here? What does it communicate or improve?"

If the answer is "because it's pretty", consider removing it.

---

## Decision Framework When Two Options Compete

Evaluate in this strict order:

1. **Usability** — Which one reduces the risk of confusion or error the most?
2. **Hierarchy** — Which one better communicates relative importance?
3. **Accessibility** — Which one is usable by the most people?
4. **Consistency** — Which one respects patterns already established in the interface?
5. **Aesthetics** — Which one is the most beautiful, given equal criteria on the previous 4 points?

Aesthetics is the **last criterion**, not the first.

---

## Minimize Usability Risks (Practical UI)

Base design decisions on risk: **what is the probability that a user will struggle with this element?**

### Frequent Risks to Identify Before Finishing a Design
- Light gray text on white background → readability risk for visually impaired
- Icon without label → misunderstanding risk (especially for cognitive disorders)
- Title text in color → confusion risk with a link
- Form fields without visible border → risk of not identifying as interactive field
- Button without visible focus state → keyboard inaccessibility risk

### Recommended Process
Before any user testing, identify and correct obvious risks. User testing serves to reveal subtle risks, not gross risks that can be resolved by common sense.