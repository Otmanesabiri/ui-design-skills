# 03 — Color System

Sources: Refactoring UI ch.4 (Color) · Practical UI ch.3 (Colour)

> **Note:** This file describes strategic concepts. For exact mathematical formulas and programmatic palette generation (JS/CSS), see `couleur-math.md`.

---

## HSL: The Right Format

Use **HSL** (Hue, Saturation, Lightness) for the web, not HEX or RGB.

| Component | Description | Values |
|---|---|---|
| **Hue** | Position on the color wheel | 0°–360° (0=red, 120=green, 240=blue) |
| **Saturation** | Intensity of the color | 0% (gray) → 100% (vibrant) |
| **Lightness** | Brightness | 0% (black) → 50% (pure) → 100% (white) |

> Do not confuse HSL and HSB. HSB is used in design tools (Figma), HSL is what the browser understands. 100% brightness and 100% saturation in HSB = 100% saturation and 50% lightness in HSL.

---

## Complete Palette Structure

### The Three Necessary Categories

**1. Grays (the majority of the interface)**
Text, backgrounds, panels, borders, inputs — almost everything is gray.
Plan for **8-10 shades**. Three or four are never enough.

```css
--gray-50:  hsl(220, 14%, 97%);
--gray-100: hsl(220, 13%, 93%);
--gray-200: hsl(220, 12%, 86%);
--gray-300: hsl(220, 11%, 74%);
--gray-400: hsl(220, 10%, 60%);
--gray-500: hsl(220, 9%,  46%);
--gray-600: hsl(220, 10%, 36%);
--gray-700: hsl(220, 12%, 26%);
--gray-800: hsl(220, 14%, 16%);
--gray-900: hsl(220, 16%, 8%);
```

**2. Primary Color(s)**
The brand color. 8-10 shades as well.

**3. Accent Colors (Semantic)**
For system states and communications:
- **Red**: error, destructive action
- **Green**: success, positive
- **Yellow/Orange**: warning
- **Blue**: information, link
- **Brand color**: highlighted feature, CTA

Each accent color needs **5-10 shades** too.

---

## Creating a Color Shade: Method

### Step 1: Choose the Base Color
The color that would work well as a button background. No fixed lightness rule — trust your eye.

### Step 2: Find the Extremes
- **Darkest shade** (900): for colored text on white background
- **Lightest shade** (50-100): for alert or tag backgrounds

### Step 3: Fill the Intermediates
Name shades 100 to 900 (or 50 to 950). 9 levels is ideal.
```
50  → ultra-light (alert backgrounds)
100 → light (tag backgrounds)
200 → light-medium
300 → medium-light
400 → medium
500 → base (standard button)
600 → medium-dark
700 → dark (hover state)
800 → very-dark (text on colored background)
900 → darkest (title on colored background)
```

### Caution: Saturation Decreases with Lightness
As a color approaches 0% or 100% lightness, saturation seems less intense. **Increase saturation** for very light and very dark shades to maintain vibrancy.

---

## Hue Rotation to Create Depth

Rather than adjusting lightness alone, **rotate the hue** towards colors that are intrinsically bright/dark.

- To **lighten**: rotate towards 60° (yellow), 180° (cyan), or 300° (magenta)
- To **darken**: rotate towards 0° (red), 120° (green), or 240° (blue)

Do not exceed 20-30° of rotation or the color will look like a different color.

**Example for yellow:**
Rather than darkening by reducing lightness (→ dull brown), rotate the hue towards orange while darkening → warm and rich result.

---

## Saturated Grays: Not Real Grays

Real grays (0% saturation) feel cold and artificial. Interface grays are slightly saturated.

### Gray Temperature
- **Cool grays**: blue tint (hsl(220, 10-15%, ...))
- **Warm grays**: orange/yellow tint (hsl(35, 10-15%, ...))

Maintain consistent temperature throughout the interface. Do not mix cool and warm grays without reason.

---

## Contrast (WCAG 2.1 level AA — mandatory)

| Context | Minimum Ratio |
|---|---|
| Normal text < 18px (or bold < 14px) | **4.5:1** |
| Large text ≥ 18px (or bold ≥ 14px) | **3:1** |
| UI Components, input borders, icons | **3:1** |
| Decorative text, logos, inactive elements | No requirement |

### Verification Tools
- [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/)
- [Colour Contrast Analyser](https://www.tpgi.com/color-contrast-checker/)
- Figma Plugin: Stark

---

## Text on Colored Background: Two Approaches

### Approach 1: Invert Contrast
Rather than white text on dark colored background (very present, overwhelming) → **dark colored text on very light colored background**.

```css
/* Information alert */
background: hsl(220, 80%, 96%);  /* very light blue */
color: hsl(220, 60%, 30%);       /* dark blue */
```

### Approach 2: Hue Rotation for Accessibility
When having colored text on a colored background, increase contrast by rotating the hue towards a brighter color (yellow, cyan, magenta) rather than just going towards white.

---

## Text on Background Image: 4 Techniques

**1. Semi-transparent Overlay**
```css
background: linear-gradient(rgba(0,0,0,0.5), rgba(0,0,0,0.5)), url('image.jpg');
```

**2. Reduce Image Contrast**
Lower contrast (-30 to -50%) and adjust brightness to compensate.

**3. Colorize the Image**
- Reduce contrast
- Desaturate (grayscale)
- Apply a solid fill in "multiply" mode

**4. Text Shadow**
```css
text-shadow: 0 0 20px rgba(0,0,0,0.6);  /* glow, not a real shadow */
```

---

## Never Use Color Alone

Color is blind to colorblind people (8% of men are red-green colorblind).

**Always back up color with:**
- An icon (✓ ✗ ⚠)
- Text ("Success", "Error", "Warning")
- A different shape or pattern

```html
<!-- Bad: color alone -->
<span style="color: red">●</span> Error

<!-- Good: color + icon -->
<span style="color: red">✗</span> Validation error
```

---

## Apply Brand Color

### 1 Brand Color = All Interactive Elements

Brand color applies to:
- Primary buttons (background)
- Links (text)
- Focus states (outline)
- Selected checkboxes and radios
- Active tabs
- Progress indicators

### Gray Palette: Tint with Brand Color
Add a slight tint of the brand color to grays to maintain visual consistency.
```css
/* Gray slightly tinted with blue (blue brand) */
--gray-500: hsl(220, 9%, 46%);   /* not hsl(0, 0%, 46%) */
```

---

## Design in Black and White First

Systematic rule: **finalize layout, hierarchy, and spacing in grayscale before adding color**.

**Important Nuance:** Design in black and white for *structure*, but allow color for *state* (Success, Pending, Error) in complex flows where it acts as a fast cognitive shortcut.

Benefits:
- Forces usage of spacing and contrast as only levers
- Reveals hierarchy problems before they are masked by color
- Produces a more visually robust interface

---

## Dark Mode: The HSL Advantage

By using HSL, creating a Dark Mode doesn't require recreating a palette from scratch. You just need to **inverse Lightness** while keeping the same Hue and Saturation.

### Dark Mode: HSL Advantage

By using HSL, creating a Dark Mode is logical, but **be careful: simply inverting Lightness is not enough**.

### HSL Mirroring Rule
A simple inversion (e.g., `100` becomes `800`) creates colors that are too saturated and aggressive on a dark background.
You must apply the **HSL Mirroring** method:
1. **Lightness**: Invert (a very light background becomes very dark).
2. **Saturation**: Reduce by 10% to 30% to avoid optical vibration.
3. **Hue**: Shift slightly (15-30°) for a richer look.

> 👉 For exact HSL Mirroring calculation formulas, see `couleur-math.md` and elevation principles in `mode-sombre.md`.

### Semantic Colors in Dark Mode:
Caution: Do not invert semantic colors (success, error, brand) the same way as surfaces. A primary button must remain identifiable (often around 500-600 lightness).
- Slightly darken alert backgrounds.
- Keep alert text readable by increasing its lightness.