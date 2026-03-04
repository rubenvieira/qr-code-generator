# Bento Dashboard — Design System v5

This document outlines the architecture, colors, typography, layout, and component styles for the QR Code Studio project.

## Core Aesthetic

A **multi-card Bento Dashboard** where each section is its own visually distinct panel floating on a rich, textured background. Inspired by Notion, Linear, and Apple design language.

*   **Light Mode:** Warm off-white mesh gradient background with subtle dot grid. Individual cards float with soft shadows and rounded corners. Pastel accent gradients. Premium, spacious, and playful.
*   **Dark Mode:** Deep charcoal mesh gradient with muted dot grid. Cards use dark surfaces. Pastel accents shift to muted jewel tones. Shadows deepen for depth.

## Architecture — Multi-Card Bento Layout

The fundamental structural principle: `.Qr-outer` is a **transparent grid container** (no background, no border, no shadow). Each child section is its own independent card with its own surface, border, shadow, and padding.

### DOM Structure (Fixed — React Bundle)

```
.App > .App-header > .Layout > .Qr-outer
  ├─ Child 1: .Qr-Centered           (Header card)
  ├─ Child 2: .Qr-titled#Qr-style    (Style picker card)
  ├─ Child 3: .Qr-titled-nobg        (Parameters card)
  ├─ Child 4: .Qr-titled             (Preview + Export card)
  ├─ Child 5: (no-op, hidden)
  └─ Child 6: (no-op, hidden)
```

Children 5-6 are broken React components (return function refs). Hidden with `display: none`.

### Page Background

Rich mesh gradient with dot grid overlay:

```
body: radial-gradient mesh (purple 15% top-left, teal 85% bottom-right)
.App-header::before: dot grid (24px spacing, 1px dots)
```

### Desktop (>=768px): Two-Column Grid of Cards

```
+─────────────────────────────────────────────────+
│  (mesh gradient background with dot grid)       │
│                                                  │
│  ┌─────────────────────────────────────────────┐ │
│  │  ✦ QR Code Studio         [Header Card]    │ │
│  │    Create beautiful QR codes                │ │
│  │    [ Enter any URL...                     ] │ │
│  └─────────────────────────────────────────────┘ │
│                                                  │
│  ┌──────────────────────┐  ┌──────────────────┐  │
│  │ ● Choose a style     │  │ ★ Export        │  │
│  │   Each one is unique │  │   Save your code│  │
│  │                      │  │                 │  │
│  │ [Pebble] [Coral]    │  │   ┌──────────┐  │  │
│  │ [Ripple] [Ivy  ]    │  │   │ QR Code  │  │  │
│  │ [Bloom ] [Ember]    │  │   │ Preview  │  │  │
│  │ ...wrapping grid     │  │   └──────────┘  │  │
│  └──────────────────────┘  │                 │  │
│                            │  [JPG] [PNG]    │  │
│  ┌──────────────────────┐  │  [SVG]          │  │
│  │ ● Customize          │  │                 │  │
│  │   Fine-tune design   │  │  (sticky)       │  │
│  │                      │  └──────────────────┘  │
│  │ Error Correction [v] │                        │
│  │ Logo Overlay     [v] │                        │
│  └──────────────────────┘                        │
│                                                  │
+──────────────────────────────────────────────────+
```

Grid: `grid-template-columns: minmax(0, 1fr) minmax(340px, 420px)`, gap: `1.25rem`

*   **Header (child 1):** Full-width (`grid-column: 1 / -1`), gradient background, centered text, rainbow accent strip.
*   **Style picker (child 2):** Left column, row 2. Wrapping gallery grid at 1200px+.
*   **Parameters (child 3):** Left column, row 3.
*   **Preview (child 4):** Right column, spans rows 2-3, `position: sticky; top: 1.5rem`. Gradient border via `::before`.

### Large Desktop (>=1200px)

*   Container widens to **1440px**
*   Card padding: **2.25rem**
*   Thumbnails: **150px**
*   Style picker: **wrapping flex grid** (all 14 styles visible at once)
*   Inputs: **320px**
*   Section titles: **1.3rem**

### Extra-Wide (>=1600px)

*   Container widens to **1560px**
*   Card padding: **2.5rem**
*   Inputs: **380px**

### Mobile (<768px): Stacked Cards with Reordering

Cards stack vertically with gap between them. Flex reordering promotes preview:

1.  **Header** (order: 1)
2.  **Style picker** (order: 2) — Horizontal scroll
3.  **Preview + Export** (order: 3) — Promoted from DOM position 4
4.  **Parameters** (order: 4) — Demoted from DOM position 3

### Small Mobile (<480px)

Reduced padding (1rem), 100px thumbnails, compact buttons, smaller text.

## Spacing & Layout Tokens

| Token | Base | 768px | 1200px | 1600px |
| ----- | ---- | ----- | ------ | ------ |
| `--layout-max-width` | 1100px | 1200px | 1440px | 1560px |
| `--card-padding` | 1.75rem | 2rem | 2.25rem | 2.5rem |
| `--grid-gap` | 1.25rem | 1.25rem | 1.25rem | 1.25rem |
| `--thumbnail-size` | 120px | 140px | 150px | — |
| `--preview-max-width` | 260px | 260px | none | — |
| `--section-title-size` | 1.05rem | 1.1rem | 1.3rem | — |
| `--input-max-width` | 220px | 260px | 320px | 380px |

### Spacing Scale

| Token | Value |
| ----- | ----- |
| `--space-xs` | 0.5rem (8px) |
| `--space-sm` | 0.75rem (12px) |
| `--space-md` | 1.25rem (20px) |
| `--space-lg` | 1.75rem (28px) |
| `--space-xl` | 2.5rem (40px) |
| `--space-2xl` | 3rem (48px) |

## Typography

*   **Sans (UI / Body / Headers):** `font-sans` ("Inter", system-ui, sans-serif)
*   **Mono (Code & Technical):** `font-mono` ("JetBrains Mono", monospace)

### Title

Gradient text via `-webkit-background-clip: text`:
```css
background: linear-gradient(135deg, var(--primary-color), var(--accent-color));
-webkit-text-fill-color: transparent;
```

Font size: `2.4rem` base, `2.8rem` at 768px+.

## Colors & Tokens

### Semantic Colors

| Token                  | Light Mode HSL       | Dark Mode HSL         | Description               |
| ---------------------- | -------------------- | --------------------- | ------------------------- |
| `--bg-color`           | `40 30% 97%`        | `240 10% 10%`         | Warm off-white / charcoal |
| `--surface-color`      | `0 0% 100%`         | `240 8% 14%`          | Card surfaces             |
| `--surface-inset`      | `40 20% 96%`        | `240 10% 11%`         | Inset input backgrounds   |
| `--text-primary`       | `240 12% 20%`       | `40 20% 92%`          | Main text color           |
| `--text-secondary`     | `240 6% 52%`        | `240 6% 58%`          | Muted / helper text       |
| `--border-color`       | `40 14% 91%`        | `240 8% 20%`          | Card borders              |
| `--dot-color`          | `40 10% 80% / 0.3`  | `240 10% 80% / 0.08`  | Dot grid pattern          |

### Accents & UI Elements

| Token                  | Light Mode HSL       | Dark Mode HSL         | Description                    |
| ---------------------- | -------------------- | --------------------- | ------------------------------ |
| `--primary-color`      | `252 56% 57%`       | `252 70% 72%`         | Primary accent (Soft Purple)   |
| `--primary-hover`      | `252 60% 50%`       | `252 65% 65%`         | Primary hover state            |
| `--primary-light`      | `252 80% 94%`       | `252 30% 18%`         | Primary tint for backgrounds   |
| `--accent-color`       | `174 52% 48%`       | `174 52% 56%`         | Secondary accent (Soft Teal)   |
| `--danger-color`       | `0 64% 58%`         | `0 64% 62%`           | Error / destructive actions    |

### Radius & Shadow Scales

| Token                 | Value/Description                        |
| --------------------- | ---------------------------------------- |
| `--radius-sm`         | `8px` — Small inputs, chips              |
| `--radius-md`         | `14px` — Inputs, buttons, small cards    |
| `--radius-lg`         | `20px` — Style thumbnails, previews      |
| `--radius-xl`         | `28px` — Section cards                   |
| `--radius-full`       | `9999px` — Pills, scrollbar thumbs       |
| `--card-shadow`       | Subtle resting shadow                    |
| `--card-shadow-hover` | Elevated hover shadow                    |

## Visual Features

### Staggered Entrance Animations

Each card animates in with a different delay using `card-rise` keyframe:
- Child 1: 0.0s delay
- Child 2: 0.1s delay
- Child 4: 0.15s delay
- Child 3: 0.2s delay

### Section Title Decorators

Each section title (`.Qr-s-title`) has a colored dot pip:
- Style picker (child 2): Purple (`--primary-color`)
- Parameters (child 3): Teal (`--accent-color`)
- Export (child 4): Amber (`hsl(38, 80%, 55%)`)

### Preview Card — Gradient Border

The preview card has a gradient border effect via `::before` pseudo-element:
```css
::before {
  inset: -2px;
  background: linear-gradient(135deg, var(--primary-color), var(--accent-color), hsl(38, 80%, 65%));
  opacity: 0.4;
  z-index: -1;
}
```

### Style Picker — Wrapping Gallery

At 1200px+, the style picker disables horizontal scrolling and wraps thumbnails into a multi-row grid showing all 14 styles at once.

### Micro-Interactions

- Style thumbnails: `translateY(-4px)` + shadow lift on hover
- Selected style: pulsing ring animation (`pulse-ring` keyframe)
- Download buttons: pill-shaped, gradient primary CTA
- Custom checkbox: `appearance: none` with purple checked state + SVG checkmark
- Upload button: purple-tinted, 48px square with hover color shift
- File upload: dashed border → solid on hover

## QR Code Styles

All 14 styles use nature-inspired names:

| Style Name | Description                                     |
| ---------- | ----------------------------------------------- |
| Pebble     | Clean and smooth, like a polished stone.        |
| Coral      | Intricate patterns inspired by ocean coral.     |
| Ripple     | Concentric rings radiating outward.             |
| Ivy        | Flowing vines that trace connected paths.       |
| Bloom      | Soft circles blooming like spring flowers.      |
| Ember      | Warm and centered, perfect for your brand mark. |
| Fern       | Scattered spores in a gentle, organic dance.    |
| Drift      | Lines dissolving like sand in the wind.         |
| Glacier    | Icy formations layered over your image.         |
| Canvas     | Your image woven into the code.                 |
| Canyon     | Deep carved pathways through layered rock.      |
| Tide       | Crossing currents that meet and merge.          |
| Aurora     | Particles fading like northern lights.          |
| Prism      | Light split into a rainbow of color.            |

## Section Copy

| Section            | Header           | Subtitle                    |
| ------------------ | ---------------- | --------------------------- |
| URL input          | —                | Paste a URL or scan a QR code |
| Style picker       | Choose a style   | Each one is unique          |
| Parameters         | Customize        | Fine-tune your design       |
| Export             | Export           | Save your code — [style]    |
| Error correction   | Error Correction | (dropdown)                  |
| Icon settings      | Logo Overlay     | Upload Logo                 |
| Color param        | Pick Color       | (popover)                   |
| Image upload       | Choose Image     | (file picker)               |

## Key CSS Classes

### Layout
*   `.Qr-outer`: **Transparent** grid container (no bg, no border, no shadow). CSS Grid on desktop, flex column on mobile.
*   `.Qr-outer > :nth-child(1-4)`: Individual section cards with own surface, border, shadow, padding.
*   `.Qr-outer > :nth-child(n+5)`: Hidden (`display: none`) — broken React components.
*   `.Qr-outer > :nth-child(4)`: Preview card — sticky, gradient border, spans 2 rows.

### Components
*   `.Qr-item-image`: Style thumbnails — token-driven size, hover lift, selected ring.
*   `.Qr-item-selected .Qr-item-image::after`: Pulsing ring animation on selected style.
*   `.Qr-table tr`: Parameter rows with inset background and rounded corners.
*   `.dl-btn`: Pill-shaped buttons (`border-radius: var(--radius-full)`).
*   `.img-dl-btn .dl-btn:first-child`: Gradient primary CTA.
*   `.Qr-checkbox`: Custom styled checkbox with SVG checkmark.
*   `.Qr-upload`: Purple-tinted 48px upload button.
*   `.ul-btn`: Dashed border file upload button.

### Responsive Breakpoints
*   `>=768px`: Two-column grid of cards, sticky preview, 1200px container.
*   `>=1200px`: 1440px container, wrapping style gallery, 150px thumbnails, 320px inputs.
*   `>=1600px`: 1560px container, 380px inputs.
*   `<768px`: Stacked cards with flex `order` reordering.
*   `<480px`: Compact (100px thumbnails, 1rem padding).
