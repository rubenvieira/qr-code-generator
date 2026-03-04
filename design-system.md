# Soft Clay / Bento — Design System

This document outlines the colors, typography, surfaces, and utility classes for the QR Code Studio project.

## Core Aesthetic

The design system embraces a warm, modern "Bento" aesthetic inspired by Notion, Linear, and Apple design language:

*   **Light Mode:** Warm off-white backgrounds, soft card shadows, pastel accent chips, generous whitespace, and rounded corners. Clean, playful, and premium.
*   **Dark Mode:** Deep charcoal surfaces with the same rounded, soft approach. Pastel accents shift to muted jewel tones. Shadows deepen for depth.

## Typography

Built around clean, modern fonts with excellent readability.

*   **Sans (UI / Body / Headers):** `font-sans` ("Inter", system-ui, sans-serif) — Used everywhere: body text, headings, buttons, labels.
*   **Mono (Code & Technical):** `font-mono` ("JetBrains Mono", monospace) — Used sparingly for technical micro-labels.

## Colors & Tokens

### Semantic Colors

| Token                  | Light Mode HSL       | Dark Mode HSL         | Description               |
| ---------------------- | -------------------- | --------------------- | ------------------------- |
| `--bg-color`           | `40 30% 97%`        | `240 10% 10%`         | Warm off-white / charcoal |
| `--surface-color`      | `0 0% 100%`         | `240 8% 14%`          | Card & container surfaces |
| `--surface-inset`      | `40 20% 96%`        | `240 10% 11%`         | Inset input backgrounds   |
| `--text-primary`       | `240 12% 20%`       | `40 20% 92%`          | Main text color           |
| `--text-secondary`     | `240 6% 52%`        | `240 6% 58%`          | Muted / helper text       |

### Accents & UI Elements

| Token                  | Light Mode HSL       | Dark Mode HSL         | Description                    |
| ---------------------- | -------------------- | --------------------- | ------------------------------ |
| `--primary-color`      | `252 56% 57%`       | `252 70% 72%`         | Primary accent (Soft Purple)   |
| `--primary-hover`      | `252 60% 50%`       | `252 65% 65%`         | Primary hover state            |
| `--primary-light`      | `252 80% 94%`       | `252 30% 18%`         | Primary tint for backgrounds   |
| `--accent-color`       | `174 52% 48%`       | `174 52% 56%`         | Secondary accent (Soft Teal)   |
| `--accent-light`       | `174 60% 92%`       | `174 30% 16%`         | Accent tint for backgrounds    |
| `--danger-color`       | `0 64% 58%`         | `0 64% 62%`           | Error / destructive actions    |

### Borders & Structural

| Token                  | Light Mode HSL       | Dark Mode HSL         | Description          |
| ---------------------- | -------------------- | --------------------- | -------------------- |
| `--border-color`       | `40 14% 89%`        | `240 8% 20%`          | Default borders      |
| `--border-color-focus` | `252 56% 57%`       | `252 70% 72%`         | Focus ring (purple)  |

### Pastel Accent Chips

Used for tags, badges, and micro-highlights:

| Token               | Background           | Text                  |
| -------------------- | -------------------- | --------------------- |
| `--chip-coral`       | Warm pink tint       | Coral text            |
| `--chip-lavender`    | Light purple tint    | Purple text           |
| `--chip-mint`        | Light green tint     | Green text            |
| `--chip-sky`         | Light blue tint      | Blue text             |
| `--chip-amber`       | Light amber tint     | Amber text            |

### Radius Scale

| Token            | Value    | Usage                        |
| ---------------- | -------- | ---------------------------- |
| `--radius-sm`    | `8px`    | Small inputs, chips          |
| `--radius-md`    | `14px`   | Inputs, buttons, small cards |
| `--radius-lg`    | `20px`   | Style thumbnails, previews   |
| `--radius-xl`    | `28px`   | Main container card          |
| `--radius-full`  | `9999px` | Pills, scrollbar thumbs      |

### Shadow Scale

| Token                 | Description                    |
| --------------------- | ------------------------------ |
| `--card-shadow`       | Subtle resting shadow          |
| `--card-shadow-hover` | Elevated hover shadow          |
| `--card-shadow-lg`    | Large container shadow         |

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

## Global Effects

*   **No CRT overlays** — Scanlines and noise grain are disabled.
*   **No grid background** — Clean solid background color.
*   **Soft shadows** — Cards use layered box-shadows for depth.
*   **Focus ring** — All focused elements get a `3px` purple outline ring with translucent spread.
*   **Smooth animations** — Cards rise with a spring-like cubic-bezier curve on load.

## Key CSS Classes

### Layout & Surface
*   `.Qr-outer`: Main container card with rainbow gradient top strip and rounded corners.
*   `.Qr-item-image`: Style thumbnail cards with soft shadows and rounded corners.
*   `.Qr-item-selected`: Active style gets purple border and tinted background.

### Interaction States
*   `.Qr-item:hover`: Cards lift 3px upward with enhanced shadow.
*   `.dl-btn:hover`: Buttons get purple border and light purple background tint.
*   `.dl-btn:active`: Buttons scale down slightly for tactile feedback.
*   Focus inputs get purple border with translucent purple ring.

### Typography
*   `.Qr-title`: 2.4rem, weight 800, tight letter-spacing. No text-transform.
*   `.Qr-subtitle`: 1rem, weight 400, secondary color. No text-transform.
*   `.Qr-s-title`: 1.15rem, weight 700 section headers.
*   `.Qr-item-detail`: 0.82rem, weight 600 style names below thumbnails.
