# Images & Media Guidelines

Sources: web.dev · Smashing Magazine · WCAG 2.2 (Non-text Content)

> **Agent Instruction:** Load this file ONLY when handling images, videos, or avatars. For image optimization & Core Web Vitals, see `extensions/performance-design.md`. For alt text ARIA rules, see `references/accessibilite-avancee.md`. For CSS values, reference `references/tokens.md`.

---

## Aspect Ratios by Context

| Context | Ratio | CSS | Usage |
|---------|-------|-----|-------|
| Hero / Banner | 16:9 | `aspect-ratio: 16 / 9` | Landing pages, blog headers |
| Card thumbnail | 4:3 | `aspect-ratio: 4 / 3` | Product cards, article previews |
| Square preview | 1:1 | `aspect-ratio: 1 / 1` | Avatars, grid galleries |
| Portrait | 3:4 | `aspect-ratio: 3 / 4` | User profiles, team pages |
| Wide cinematic | 21:9 | `aspect-ratio: 21 / 9` | Full-width banners |
| OG / Social share | 1.91:1 | `aspect-ratio: 1.91 / 1` | Meta tags, social previews |

### Enforcing Ratio Without Distortion

```css
.media-container {
  aspect-ratio: 16 / 9;
  overflow: hidden;
  border-radius: var(--radius-lg);
}

.media-container img,
.media-container video {
  width: 100%;
  height: 100%;
  object-fit: cover;     /* fill container, crop if needed */
  object-position: center;
}
```

### Object-fit Reference

| Value | Behavior | Use When |
|-------|----------|----------|
| `cover` | Fills container, crops excess | Photos, backgrounds |
| `contain` | Fits inside, may letterbox | Logos, diagrams |
| `fill` | Stretches to fit | ❌ Never (distorts) |
| `none` | Original size, crops if larger | Decorative textures |

---

## Avatar System

### Sizes

| Size | px | Usage |
|------|-----|-------|
| xs | 24px | Inline mentions, compact lists |
| sm | 32px | Table rows, comments |
| md | 40px | Navigation user pill, cards |
| lg | 56px | Profile headers |
| xl | 80px | Profile pages, settings |
| 2xl | 120px | Large profile view |

### Structure

```html
<!-- Image avatar -->
<img class="avatar avatar-md" src="user.webp"
     alt="Jane Doe" width="40" height="40" />

<!-- Initials fallback -->
<div class="avatar avatar-md" aria-label="Jane Doe">
  <span aria-hidden="true">JD</span>
</div>

<!-- Avatar with status indicator -->
<div class="avatar-wrapper">
  <img class="avatar avatar-md" src="user.webp" alt="Jane Doe" />
  <span class="avatar-status online" aria-label="Online"></span>
</div>
```

### CSS

```css
.avatar {
  border-radius: var(--radius-full);
  object-fit: cover;
  background: var(--color-brand-subtle);
  color: var(--color-brand);
  display: inline-flex;
  align-items: center;
  justify-content: center;
  font-weight: 600;
  flex-shrink: 0;
}

.avatar-xs  { width: 24px; height: 24px; font-size: 10px; }
.avatar-sm  { width: 32px; height: 32px; font-size: 12px; }
.avatar-md  { width: 40px; height: 40px; font-size: 14px; }
.avatar-lg  { width: 56px; height: 56px; font-size: 18px; }
.avatar-xl  { width: 80px; height: 80px; font-size: 24px; }
.avatar-2xl { width: 120px; height: 120px; font-size: 36px; }

/* Status indicator */
.avatar-wrapper { position: relative; display: inline-block; }

.avatar-status {
  position: absolute;
  bottom: 0;
  right: 0;
  width: 10px;
  height: 10px;
  border-radius: var(--radius-full);
  border: 2px solid var(--color-bg-card);
}

.avatar-status.online  { background: var(--success-500); }
.avatar-status.offline { background: var(--gray-400); }
.avatar-status.busy    { background: var(--error-500); }
```

### Avatar Group (Stacked)

```css
.avatar-group {
  display: flex;
  flex-direction: row-reverse; /* stack right-to-left */
}

.avatar-group .avatar {
  margin-left: -8px;
  border: 2px solid var(--color-bg-card);
  box-shadow: var(--shadow-xs);
}

.avatar-group .avatar:last-child {
  margin-left: 0;
}

/* "+3 more" badge */
.avatar-overflow {
  background: var(--gray-200);
  color: var(--color-text-secondary);
  font-size: 11px;
  font-weight: 700;
}
```

---

## Alt Text Rules

### Decision Tree

```
Is the image decorative (background, texture, divider)?
  → alt="" (empty alt, still required for valid HTML)

Does the image contain text?
  → alt must contain that exact text

Is the image functional (link, button)?
  → alt describes the ACTION, not the image
  → Example: alt="Go to homepage" (not alt="company logo")

Is the image informative (chart, photo, diagram)?
  → alt describes the INFORMATION conveyed
  → Example: alt="Revenue grew 23% in Q3 2025"
```

### Examples

```html
<!-- Decorative -->
<img src="pattern.svg" alt="" aria-hidden="true" />

<!-- Informative -->
<img src="chart.png"
     alt="Bar chart showing monthly revenue from Jan to Jun, peaking at $32K in April" />

<!-- Functional -->
<a href="/">
  <img src="logo.svg" alt="Forma — Go to homepage" />
</a>

<!-- User-generated content -->
<img src="upload.jpg" alt="Photo uploaded by Jane Doe on May 3, 2026" />
```

---

## Responsive Images

### srcset + sizes

```html
<img
  src="product-800.webp"
  srcset="
    product-400.webp  400w,
    product-800.webp  800w,
    product-1200.webp 1200w
  "
  sizes="
    (max-width: 640px) 100vw,
    (max-width: 1024px) 50vw,
    33vw
  "
  alt="Payment terminal device"
  width="1200" height="800"
  loading="lazy"
  decoding="async"
/>
```

### Picture Element (Format Fallback)

```html
<picture>
  <source srcset="hero.avif" type="image/avif" />
  <source srcset="hero.webp" type="image/webp" />
  <img src="hero.jpg" alt="Dashboard overview" width="1600" height="900" />
</picture>
```

---

## Placeholder Strategies

| Strategy | When | Visual |
|----------|------|--------|
| **Dominant color** | Simple, fast | Solid background matching image |
| **Blur-up (LQIP)** | Hero images, important photos | Tiny blurred version → sharp |
| **Skeleton** | Cards, avatars, thumbnails | Gray animated placeholder |
| **Silhouette** | Known shape (avatar, icon) | Shape outline |

```css
/* Skeleton for image loading */
.image-skeleton {
  background: var(--gray-200);
  animation: shimmer 1.5s infinite linear;
}

/* Blur-up transition */
.image-blur {
  filter: blur(20px);
  transform: scale(1.05); /* hide blur edges */
  transition: filter 500ms var(--ease-out),
              transform 500ms var(--ease-out);
}

.image-blur.loaded {
  filter: blur(0);
  transform: scale(1);
}
```

---

## Video Guidelines

```html
<!-- Autoplay videos: muted, no controls, decorative -->
<video autoplay muted loop playsinline
       aria-hidden="true"
       poster="video-poster.webp">
  <source src="hero.mp4" type="video/mp4" />
</video>

<!-- User-controlled video: with controls -->
<video controls preload="metadata"
       poster="video-poster.webp"
       aria-label="Product demo video">
  <source src="demo.webp" type="video/webm" />
  <source src="demo.mp4" type="video/mp4" />
  <track kind="captions" src="captions-en.vtt" srclang="en" label="English" />
</video>
```

### Rules

```
[ ] Autoplay videos MUST be muted (browser policy)
[ ] Always provide a poster image
[ ] Include captions/subtitles for content videos
[ ] Respect prefers-reduced-motion: pause autoplay videos
[ ] Never autoplay with sound
```

---

## Checklist

```
Aspect Ratios
[ ] Consistent ratio per context (16:9 heroes, 1:1 avatars)
[ ] object-fit: cover or contain used (never fill)
[ ] aspect-ratio set on container

Avatars
[ ] Initials fallback when no image
[ ] Size scale followed consistently
[ ] Status indicators use shape + color

Alt Text
[ ] Every <img> has an alt attribute
[ ] Decorative images use alt=""
[ ] Functional images describe the action
[ ] Informative images describe the content

Responsive
[ ] srcset + sizes on all photos
[ ] WebP with JPEG/PNG fallback
[ ] width + height set (prevents CLS)
[ ] loading="lazy" below the fold

Video
[ ] Poster image always present
[ ] Captions for content videos
[ ] Autoplay only if muted
```
