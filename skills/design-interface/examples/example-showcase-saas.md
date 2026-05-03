# 🏆 Showcase Example: SaaS Marketing Page — Full Power Demonstration

> **Purpose:** This example exists to prove what this skill produces when used at full capacity.
> It is NOT a description of what to do. It is a real, executable prompt + the actual result.
> Copy the prompt below into any AI agent with this skill loaded to reproduce the output.

---

## The Prompt

```
/generate-ui

Build a complete SaaS marketing page for "Forma" — a B2B analytics platform that 
helps e-commerce teams track their revenue metrics in real time.

Target user: Head of Growth / Data Analyst at a 50-500 person e-commerce company.
Primary fear: losing revenue because they can't see what's happening fast enough.
Primary desire: feel in control of their numbers, impress their CEO.

Brand direction: dark, premium, data-forward. Not playful. Not corporate.
Think: Linear meets Vercel meets Stripe. Confident, minimal, fast.

Mandatory constraints from the skill:
- Apply the full Page Contract for SaaS Marketing Page (all 8 sections)
- Design in grayscale mentally first, then apply brand color
- Brand color: electric indigo — hsl(248, 90%, 62%)
- All tokens from references/tokens.md (4px grid, HSL palette, shadow scale)
- All UX laws enforced and cited in code comments
- Micro-interactions on every interactive element (Doherty Threshold: < 400ms)
- Full accessibility: WCAG AA contrast, aria-labels, focus states, keyboard nav
- No dark patterns, no fake urgency, no fake numbers
- Sections must flow as one seamless narrative, not disconnected blocks
- Ship production-ready HTML + CSS. Zero placeholder content.
```

---

## What the Skill Forces the Agent to Do

Before writing a single line of code, the agent **must** resolve:

### Step 0 — Page Contract (SaaS Marketing Page)
Sections locked by convention (Jakob's Law — users expect these):
1. Navigation (sticky, blur on scroll)
2. Hero (product claim + visual proof + CTA)
3. Features (3 differentiators, not 7)
4. How It Works (3-step process, not a wall of text)
5. Pricing (3 tiers, middle highlighted via Von Restorff)
6. Testimonials (2-3 quotes, real roles, no fake names)
7. CTA Band (single conversion moment)
8. Footer (structured, no visual noise)

### Step 1 — Frame Before Drawing
- **Who:** Head of Growth, 35yo, lives in dashboards, has 3 browser tabs open at all times
- **Main action:** Start a free trial
- **Main risk:** "This looks like every other tool" → No trust → No conversion
- **Kill it with:** Immediate product proof in the hero (not just words), real numbers

### Step 2 — Token Application
- Brand: `hsl(248, 90%, 62%)` → indigo-500
- Dark surface: `hsl(222, 20%, 9%)` (not pure black — blue-tinted per couleur-systeme.md)
- Semantic gray scale: cool grays tinted with hsl(220) to match brand temperature
- Typography: `clamp(52px, 7vw, 80px)` for hero H1, `--leading-none` (1.0)
- Section gap: `--space-32` (128px) — breathing room signals confidence
- Animations: `--ease-spring` on cards, `--ease-out` on page entries, all ≤ 300ms

---

## Expected Output Characteristics

A senior designer reviewing this output should say:

> "This feels like it was designed by a team, not generated."

Measurable signals:
- [ ] Hero H1 is specific, not generic ("See your revenue drop before your CEO does")
- [ ] Product visual is present in the first viewport (not just text)
- [ ] The pricing section has one obvious "recommended" tier (Von Restorff)
- [ ] Hover states exist on every card, button, and link
- [ ] The page reads at desktop AND collapses correctly at 375px
- [ ] Zero emojis used as design elements
- [ ] Zero gradient-on-gradient backgrounds
- [ ] Comment in code cites the UX law for each decision

---

## Actual Output

> The HTML file produced by this prompt is saved at:
> `examples/showcase-saas-output.html`
>
> Open it in a browser. This is what the skill delivers.
