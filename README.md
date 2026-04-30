<div align="center">
  <img src="img/cover1.png" alt="UI Design Skills Framework Cover" width="400px">
  
  <h1>UI Design Skills Framework</h1>
  
  <p><strong>The Science of Interface Design for Engineers</strong></p>
</div>

<br />

Developing modern interfaces is challenging. Without a systematic approach, developers often resort to "vibe coding" CSS—randomly tweaking pixels until the layout "looks right." The inevitable result is visual technical debt, inconsistent component libraries, and a frustrating user experience.

The **UI Design Skills Framework** is engineered to transform interface design into an iterative, predictable science. It eliminates choice paralysis by enforcing strict design token systems (HSL color spaces, 4px spatial grids) and rooting every design decision in established psychological principles (Jakob's Law, Hick's Law, Miller's Law).

---

## 🚀 Quickstart

Initialize the framework in your agent's environment in seconds:

```bash
npx skills@latest add otmanesabiri/ui-design-skills
```

Once added, select the desired skills and the agents you want to attach them to. Run the `/setup-otmanesabiri-skills` command in your agent's chat to bootstrap the environment. This script will automatically:

1. **Bootstrap Design Tokens:** Configure your HSL color palettes and spatial scales.
2. **Enforce Accessibility:** Establish WCAG AA compliance baselines for contrast ratios.
3. **Inject Component References:** Load best practices for buttons, forms, and complex data tables.

You are now ready to engineer professional-grade interfaces.

---

## 🧠 Why This Framework Exists

This repository was built to systematically eradicate the critical mistakes that 90% of developers make when architecting frontends.

### 1. Defeating Choice Paralysis
> *"The time it takes to make a decision increases with the number and complexity of choices."* — **Hick's Law**

**The Problem:** Staring at a blank canvas, developers waste time debating hex codes and padding values. This indecision cripples development velocity and shatters visual consistency.
**The Solution:** **Strict Design Tokens**. We eliminate arbitrary values. Every color, shadow, and margin is pulled from a predefined, mathematically sound scale.
*→ Use the `/generate-ui` command to scaffold layouts using fixed scales.*

### 2. Accessibility as a Foundation, Not an Afterthought
**The Problem:** Contrast ratios and touch target sizes are typically audited at the end of a project, when refactoring is most expensive.
**The Solution:** **Accessibility by Design**. Constraints like 44x44px minimum touch targets and WCAG AA contrast ratios are hardcoded into the foundation of the generation process.
*→ Use the `/review-ui` command for an immediate, severity-based accessibility audit.*

### 3. Mitigating Cognitive Overload
**The Problem:** Dense dashboards frequently become unusable because they violate Miller's Law (the average person can only keep ~7 items in their working memory).
**The Solution:** **Strategic Chunking**. The framework enforces grouping related information to drastically reduce mental load.
*→ Integrated directly into the patterns for **Complex Data Tables** and **Dashboards**.*

### 4. Eradicating Static Interfaces
**The Problem:** Interfaces lacking micro-interactions feel unresponsive, broken, or "dead" (violating the Doherty Threshold).
**The Solution:** **Standardized Motion Tokens**.
*→ Enforced transition durations (100ms - 300ms) and spring easing curves (`--ease-spring`) guarantee an interface that feels snappy and alive.*

---

## 🛠️ Tooling & Commands

### Interface Engineering
Tools for your daily UI development workflow:

*   **`/generate-ui`** — Executes a complete creation pipeline: feature framing, grayscale visual hierarchy establishment, and finally, the application of brand colors and micro-interactions.
*   **`/improve-ui`** — Refactors an existing interface. It ruthlessly prioritizes blocking usability issues and structural flaws before addressing aesthetic polish.
*   **`/review-ui`** — Conducts a rigorous, structured audit based on a severity grid (Blocking, Major, Minor). Every critique is backed by citing specific UX Laws.

### Systems & Foundations
*   **Dark Mode (HSL Mirroring)** — An intelligent lightness-inversion algorithm for flawless dark modes, eliminating the need to manually redefine palettes.
*   **Design Tokens** — Concrete, scalable values for spacing (4px base), fluid typography, semantic shadows, and z-index elevations.
*   **UX Laws Library** — A built-in knowledge base codifying Jakob's, Fitts's, Hick's, and Miller's Laws, alongside the Doherty Threshold.

---

<div align="center">
  <p><em>Software engineering demands rigor. Interface design requires no less.</em></p>
  <p>This framework condenses decades of design principles (drawing heavily from <em>Refactoring UI</em> and <em>Practical UI</em>) into repeatable, automated practices, empowering you to ship the most professional products of your career.</p>
</div>
