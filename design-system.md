# Soft Clay / Bento — Design System v3

This document outlines the colors, typography, layout, and utility classes for the QR Code Studio project.

## Core Aesthetic

The design system embraces a warm, modern "Bento" aesthetic inspired by Notion, Linear, and Apple design language:

*   **Light Mode:** Warm off-white backgrounds, soft card shadows, pastel accent chips, generous whitespace, and rounded corners. Clean, playful, and premium.
*   **Dark Mode:** Deep charcoal surfaces with the same rounded, soft approach. Pastel accents shift to muted jewel tones. Shadows deepen for depth.

## Layout

### Desktop (>=768px): Two-Column Grid

The main container (`.Qr-outer`) uses CSS Grid with two columns:

*   **Left column (`minmax(0, 1fr)`):** Header, URL input, style picker, customization parameters. The `minmax(0, 1fr)` prevents horizontal scroll content (style picker) from expanding beyond the column.
*   **Right column (`340px`):** QR preview + export buttons in a sticky panel with inset background.
*   **Gap:** `0 2rem` (32px horizontal, no vertical gap — sections handle their own spacing).

The right column stays visible as the user scrolls through options on the left via `position: sticky`.

**Key technical details:**
*   `overflow: clip` on `.Qr-outer` — clips content to preserve `border-radius` on the gradient strip, but unlike `overflow: hidden`, does **not** create a scroll container, so `position: sticky` still works inside the grid.
*   `min-width: 0` on all grid children — prevents flex/grid items from expanding beyond their column when containing scrollable content.

```
+-----------------------------------------------+
| Rainbow gradient strip                        |
+----------------------------+------------------+
| Header / Title             |                  |
| URL Input                  |                  |
+----------------------------+  QR Preview      |
| Choose a style             |  (sticky)        |
| [style] [style] [style]>> |  (fluid width)   |
+----------------------------+                  |
| Customize                  |  Export buttons  |
| Error Correction  [15%  v] |  JPG PNG SVG     |
| Logo Overlay      [None v] |                  |
+----------------------------+------------------+
```

### Mobile (<768px): Flex Column with Reordering

On mobile, `.Qr-outer` switches to `display: flex; flex-direction: column` with CSS `order` to promote the preview above parameters:

1.  **Header** (order: 1) — Title + URL input
2.  **Style picker** (order: 2) — Horizontal scrolling style cards
3.  **Preview + Export** (order: 3) — QR preview and download buttons (promoted from DOM position 4)
4.  **Parameters** (order: 4) — Customization options (demoted from DOM position 3)

This ensures users see their QR code immediately after selecting a style, without scrolling past parameter tables.

### Small Mobile (<480px): Compact

Reduced padding (1rem container), smaller style thumbnails (100x100px), compact buttons, smaller text.

## Typography

*   **Sans (UI / Body / Headers):** `font-sans` ("Inter", system-ui, sans-serif)
*   **Mono (Code & Technical):** `font-mono` ("JetBrains Mono", monospace)

## Colors & Tokens

### Semantic Colors

| Token                  | Light Mode HSL       | Dark Mode HSL         | Description               |
| ---------------------- | -------------------- | --------------------- | ------------------------- |
| `--bg-color`           | `40 30% 97%`        | `240 10% 10%`         | Warm off-white / charcoal |
| `--surface-color`      | `0 0% 100%`         | `240 8% 14%`          | Card & container surfaces |
| `--surface-inset`      | `40 20% 96%`        | `240 10% 11%`         | Inset input backgrounds   |
| `--text-primary`       | `240 12% 20%`       | `40 20% 92%`          | Main text color           |
| `--text-secondary`     | `240 6% 52%`        | `240 6% 58%`          | Muted / helper text       |
| `--divider-color`      | `40 14% 91%`        | `240 8% 18%`          | Section divider lines     |

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
| `--radius-xl`         | `28px` — Main container card             |
| `--radius-full`       | `9999px` — Pills, scrollbar thumbs       |
| `--card-shadow`       | Subtle resting shadow                    |
| `--card-shadow-hover` | Elevated hover shadow                    |
| `--card-shadow-lg`    | Large container shadow                   |

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

User-facing labels use friendly, approachable language:

| Section            | Header           | Subtitle                    |
| ------------------ | ---------------- | --------------------------- |
| Style picker       | Choose a style   | Each one is unique          |
| Parameters         | Customize        | Fine-tune your design       |
| Export             | Export           | Save your code — [style]    |
| Error correction   | Error Correction | (dropdown)                  |
| Icon settings      | Logo Overlay     | Upload Logo                 |
| Color param        | Pick Color       | (popover)                   |
| Image upload       | Choose Image     | (file picker)               |

## Key CSS Classes

### Layout
*   `.Qr-outer`: Main container — CSS Grid on desktop (`minmax(0, 1fr) 340px`), flex column on mobile with `order` reordering. Uses `overflow: clip` to preserve border-radius clipping while allowing sticky positioning.
*   `.Qr-outer > :nth-child(4)`: Preview column — sticky (`top: 2rem`), inset background, centered content.
*   `.Qr-titled` / `.Qr-titled-nobg`: Section wrappers with top border dividers.
*   All grid children: `min-width: 0` to prevent content overflow beyond grid columns.

### Components
*   `.Qr-item-image`: Style thumbnail cards — 140x140px on desktop, 120x120px on tablet, 100x100px on small mobile. Rounded corners, shadow.
*   `.Qr-item-selected`: Active style gets purple border, tinted background, focus ring.
*   `.Qr-div-table`: Parameter table wrapper. Labels left-aligned on desktop.
*   `.btn-row` / `.img-dl-btn`: Export button group wrappers. Full-width on mobile.
*   `.dl-btn`: Standard outlined button (min-height 44px for touch targets).
*   `.img-dl-btn .dl-btn:first-child`: Primary filled CTA (purple background, white text).
*   `.ul-btn`: Upload button variant.
*   `.Gray`: Muted superscript for download counts.
*   `.note-font`: Small note text.
*   `#dl-image-inner`: QR preview — fluid width (`width: 100%`), constrained by container padding.

### Interaction States
*   `.Qr-item:hover`: Cards lift 3px with enhanced shadow.
*   `.dl-btn:hover`: Purple border + light purple background tint.
*   `#dl-image-inner:hover`: Preview lifts 2px with purple border.
*   Focus inputs: Purple border with translucent purple ring (`3px`).

### Responsive Breakpoints
*   `>=768px`: Two-column grid (`minmax(0, 1fr) 340px`), sticky preview, wider container (1080px), 140px thumbnails, tighter section spacing.
*   `<768px`: Flex column with `order` reordering (preview promoted above parameters), full-width buttons, 120px thumbnails.
*   `<480px`: Compact (100px thumbnails, 1rem padding, smaller text, reduced gaps).
