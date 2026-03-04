# Soft Clay / Bento — Design System v2

This document outlines the colors, typography, layout, and utility classes for the QR Code Studio project.

## Core Aesthetic

The design system embraces a warm, modern "Bento" aesthetic inspired by Notion, Linear, and Apple design language:

*   **Light Mode:** Warm off-white backgrounds, soft card shadows, pastel accent chips, generous whitespace, and rounded corners. Clean, playful, and premium.
*   **Dark Mode:** Deep charcoal surfaces with the same rounded, soft approach. Pastel accents shift to muted jewel tones. Shadows deepen for depth.

## Layout

### Desktop (>=768px): Two-Column Grid

The main container uses CSS Grid with two columns:

*   **Left column (flexible):** Header, URL input, style picker, customization parameters
*   **Right column (320px):** QR preview + export buttons in a sticky panel with inset background

The right column stays visible as the user scrolls through options on the left.

```
+-----------------------------------------------+
| Rainbow gradient strip                        |
+----------------------------+------------------+
| Header / Title             |                  |
| URL Input                  |                  |
+----------------------------+  QR Preview      |
| Choose a style             |  (sticky)        |
| [style] [style] [style]>> |                  |
+----------------------------+  Export buttons  |
| Customize                  |  JPG PNG SVG     |
| Error Correction  [15%  v] |                  |
| Logo Overlay      [None v] |                  |
+----------------------------+------------------+
```

### Mobile (<768px): Single Column

Everything stacks vertically. The QR preview appears inline between parameters and export buttons.

### Small Mobile (<480px): Compact

Reduced padding, smaller style thumbnails (100x100px), compact buttons.

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
*   `.Qr-outer`: Main container — CSS Grid on desktop, single column on mobile.
*   `.Qr-outer > :nth-child(4)`: Preview column — sticky, inset background, centered content.
*   `.Qr-titled` / `.Qr-titled-nobg`: Section wrappers with top border dividers.

### Components
*   `.Qr-item-image`: Style thumbnail cards (120x120px), rounded corners, shadow.
*   `.Qr-item-selected`: Active style gets purple border, tinted background, focus ring.
*   `.Qr-div-table`: Parameter table wrapper.
*   `.btn-row` / `.img-dl-btn`: Export button group wrappers.
*   `.dl-btn`: Standard outlined button.
*   `.img-dl-btn .dl-btn:first-child`: Primary filled CTA (purple background, white text).
*   `.ul-btn`: Upload button variant.
*   `.Gray`: Muted superscript for download counts.
*   `.note-font`: Small note text.

### Interaction States
*   `.Qr-item:hover`: Cards lift 3px with enhanced shadow.
*   `.dl-btn:hover`: Purple border + light purple background tint.
*   `#dl-image-inner:hover`: Preview lifts 2px with purple border.
*   Focus inputs: Purple border with translucent purple ring (`3px`).

### Responsive Breakpoints
*   `>=768px`: Two-column grid, sticky preview, wider container (1080px).
*   `<768px`: Single column, centered inputs, full-width tables.
*   `<480px`: Compact (smaller thumbnails, reduced padding, smaller buttons).
