# Example: E-commerce Landing Page Generation

**User Request:** "Build a landing page for a sports shoe store."

## Agent Response (Based on UI Skills)

### 0. Page Contract Resolution

- **Confirmed page type:** E-commerce Landing Page
- **Implicit sections to build (in order):**
  1. Navigation (fixed, transparent on scroll)
  2. Hero (product image + H1 + primary CTA)
  3. Features / Technology (3 key differentiators)
  4. Product Grid (3–4 featured products)
  5. Social Proof (brand logos or testimonials)
  6. Promo / Urgency band (optional discount or limited offer)
  7. Newsletter section
  8. Full footer (links, legal, socials)
- **No user restriction detected** — full contract applies.

### 1. Analysis and Hierarchy (Grayscale First)

Core user task: **discover the product → decide → buy**.

Priority order:
1. Hero: product name + visual + price signal + CTA
2. Trust signals: features, reviews, brand logos
3. Browsable products: scannable grid
4. Conversion support: newsletter, promo, footer

### 2. Token Application

- **Brand color:** Neon accent on dark background for sports energy.
- **Typography:** Display scale (`clamp(48px, 8vw, 72px)`, `font-weight: 900`) for hero H1. Body at `--text-lg` with `color-text-secondary`.
- **Spacing:** `--space-24` (96px) between major sections. `--space-8` (32px) between cards.
- **Cards:** `--color-bg-card` with `--shadow-md`, `--radius-xl`, hover `translateY(-8px)` with `--ease-spring`.
- **Animations:** Intersection Observer fade-up at `0.6s` `--ease-out`. No animation > 400ms (Doherty Law).

### 3. Sections Breakdown

```
[NAV]        Fixed — logo left, links center, CTA right
[HERO]       2-column grid: H1 + CTA left / product image right
[FEATURES]   3-column card grid with SVG icons
[PRODUCTS]   3-column product card grid with image, name, price
[BRANDS]     Horizontal logo bar (opacity 0.5, hover 1)
[PROMO]      Full-width band with accent background + CTA
[NEWSLETTER] 2-column: H2 left / email form right
[FOOTER]     4-column grid: brand info, shop links, help, company
```

### 4. Non-Negotiable Rules Applied

- SVG icons used throughout (no emojis, no emoji fallback).
- `aria-hidden="true"` on all decorative SVGs.
- All interactive elements: `min-height: 44px` (Fitts's Law).
- Navigation scroll behavior: `backdrop-filter: blur()` activated on `window.scrollY > 60`.
- No fake urgency timers or unverifiable social proof numbers (Ethical Design).
- Primary CTA: one per viewport. "Explore Collection" in hero, no competing equal-weight CTA.

### 5. Expected Result

A dark-themed, high-energy landing page with a strong typographic presence in the hero. The product image anchors the right column. Below, three feature cards lift on hover. The product section uses real imagery with subtle visual differentiators between cards (color, opacity). The page feels complete and commercially credible by covering all eight conventional sections of an e-commerce landing page.
