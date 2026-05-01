# Dark Mode (HSL Mirroring)

Creating an effective dark mode is not simply about inverting black and white. The "HSL Mirroring" system allows for a logical and mathematical transition of colors.

## 1. The Problem with Traditional Dark Modes
- **Too much contrast:** Pure white text (`#FFFFFF`) on a pure black background (`#000000`) strains the eyes.
- **Unadapted colors:** Saturated colors (e.g., a bright red) vibrate on a dark background and become difficult to look at.
- **Lost depth:** In light mode, we use shadows to create elevation. In dark mode, shadows are invisible; we must use surface brightness to indicate elevation.

## 2. The Solution: HSL Mirroring
By using the HSL (Hue, Saturation, Lightness) format, we can invert the palette consistently:

### Lightness
- In light mode, the background is near 100% L (e.g., 98%), and text is near 0% L (e.g., 10%).
- In dark mode, the background should be dark (e.g., 10% L to 15% L) and the text light (e.g., 85% L to 90% L).

### Saturation
- **Golden Rule:** In dark mode, reduce the saturation of accent colors (blue, red, etc.) to prevent them from vibrating or being too aggressive.

## 3. Surface Implementation
In dark mode, the closer an element is to the user (elevation), the **lighter** it must be.

- `surface-1` (Background): `hsl(var(--hue) 10% 10%)`
- `surface-2` (Card): `hsl(var(--hue) 10% 14%)`
- `surface-3` (Modal/Dropdown): `hsl(var(--hue) 10% 18%)`

## 4. Dark Mode Checklist
- [ ] Background is not pure black (`#000000`), but rather a very dark or tinted gray (`#121212`).
- [ ] Text is not pure white (`#FFFFFF`), but slightly softened (e.g., `rgba(255, 255, 255, 0.87)`).
- [ ] Accent colors have been desaturated to remain readable without straining the eye.
- [ ] Elevation is represented by lightening surfaces, not by shadows (although subtle black shadows can still mark edges).
