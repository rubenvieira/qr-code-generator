# Retro Instrument Panel & CRT Command Center Design System

This document outlines the colors, typography, effects, and utility classes for the project, allowing you to use this design system across all tools.

## Core Aesthetic

The design system embraces a dual-theme aesthetic:
*   **Light Mode:** "Day Shift" Instrument Panel — tactile, physical hardware with inset panels, raised surfaces, and sharp edges.
*   **Dark Mode:** "CRT Command Center" — glowing phosphor screens with scanlines, CRT artifacts, and deeply atmospheric dark UI.

## Typography

The typography is built around utilitarian, technical fonts.

*   **Sans (UI / Body):** `font-sans` ("IBM Plex Sans", system-ui, sans-serif) - Used for general text.
*   **Display (Headers):** `font-display` ("Chakra Petch", system-ui, sans-serif) - Used for `h1`, `h2`, `h3`.
*   **Mono (Code & Labels):** `font-mono` ("IBM Plex Mono", monospace) - Used for precise metrics and technical labels.

## Colors & Tokens

The color system uses HSL values mapped to Tailwind CSS variables. Most surface and base colors shift significantly between light and dark modes to sell the physical vs. digital aesthetics.

### Semantic Colors

| Token                  | Light Mode HSL | Dark Mode HSL | Description |
| ---------------------- | -------------- | ------------- | ----------- |
| `--background`         | `45 20% 95%`   | `220 18% 6%`  | Main app background |
| `--foreground`         | `220 25% 12%`  | `42 30% 88%`  | Main text color |
| `--card`               | `45 15% 92%`   | `220 16% 9%`  | Card background |
| `--card-foreground`    | `220 25% 12%`  | `42 30% 88%`  | Card text |
| `--popover`            | `45 15% 92%`   | `220 18% 8%`  | Popovers, tooltips, dropdowns |
| `--popover-foreground` | `220 25% 12%`  | `42 30% 88%`  | Popover text |

### Accents & UI Elements

| Token                  | Light Mode HSL | Dark Mode HSL | Description |
| ---------------------- | -------------- | ------------- | ----------- |
| `--primary`            | `25 85% 42%`   | `38 90% 55%`  | Primary glowing accent (Amber / Orange) |
| `--primary-foreground` | `45 20% 95%`   | `220 18% 6%`  | Text appearing on primary background |
| `--secondary`          | `45 10% 88%`   | `220 12% 14%` | Secondary buttons and elements |
| `--secondary-foreground`| `220 20% 20%` | `42 20% 75%`  | Text appearing on secondary background |
| `--muted`              | `45 10% 88%`   | `220 12% 14%` | Disabled or less important elements |
| `--muted-foreground`   | `220 10% 45%`  | `42 15% 55%`  | Muted text |
| `--accent`             | `170 50% 32%`  | `165 60% 45%` | Secondary glowing accent (Teal / Cyan) |
| `--accent-foreground`  | `45 20% 95%`   | `220 18% 6%`  | Text appearing on accent background |
| `--destructive`        | `0 70% 45%`    | `0 70% 50%`   | Error states and destructive actions |
| `--destructive-foreground`| `0 0% 100%` | `0 0% 100%`   | Text on destructive elements |

### Borders & Structural Colors

| Token                  | Light Mode HSL | Dark Mode HSL | Description |
| ---------------------- | -------------- | ------------- | ----------- |
| `--border`             | `220 8% 80%`   | `220 12% 16%` | Default borders |
| `--input`              | `220 8% 80%`   | `220 12% 14%` | Form input borders |
| `--ring`               | `25 85% 42%`   | `38 90% 55%`  | Focus ring color (matches primary) |
| `--radius`             | `0rem`         | `0rem`        | Sharp, non-rounded edges across the app |

### Physical & Instrument Effects

| Token                  | Light Mode HSL | Dark Mode HSL | Notes |
| ---------------------- | -------------- | ------------- | ----- |
| `--glow-amber`         | `25 85% 42%`   | `38 90% 55%`  | Tactical amber used for hover and active glow states |
| `--glow-teal`          | `170 50% 32%`  | `165 60% 45%` | Tactical teal used for contrast accents |
| `--surface-raised`     | `45 15% 97%`   | `220 14% 12%` | Raised physical hardware look |
| `--surface-inset`      | `45 12% 89%`   | `220 20% 5%`  | Sunken/pressed physical hardware look |
| `--grid-line`          | `220 8% 85%`   | `220 12% 14%` | Plotting and background grids |
| `--scanline`           | `220 25% 12%`  | `0 0% 100%`   | CRT artifact color tint over screen |

## Global Overlays & Artifacts

*   **Subtle Noise Grain:** A faint constant fractal noise exists over the screen acting like a plastic micro-texture in light mode and digital static in dark mode.
*   **CRT Scanlines (Dark Mode):** A repeating linear gradient adds faint horizontal TV scanlines.
*   **Focus Ring:** All focused interactive elements have a tactile `2px solid var(--primary)` outline offset by `2px`.

## Utility Classes & Components

### Layout & Surface
*   `.retro-card`: Standard component container. Features a subtle amber 2px left border strip that expands on hover, casting an amber box shadow.
*   `.inset-panel`: Uses `--surface-inset` with inner background shadow giving it a sunken, cut-out look (great for logs or form inputs).
*   `.raised-panel`: Uses `--surface-raised` with a lighter top border mimicking light hitting a physical raised edge.
*   `.amber-border-left`: A quick left amber border.
*   `.teal-border-left`: A quick left teal border.
*   `.instrument-divider`: Adds a 1px divider spanning the container width, flanked by tiny 7px vertical tick marks on both edges. Perfect for separating controls.

### Typography Elements
*   `.mono-label`: Sets text to the mono font, `11px` uppercase, with tight letter spacing block (`0.2em`). Ideal for tiny technical micro-labels above inputs or gauges.

### Interaction States & Animations
*   `.retro-glow`: Element emits a subtle amber box-shadow glow on hover.
*   `.btn-press`: Provides a physical tactile pushed-button feel. The element scales down to 98% and receives a harsh top inner shadow on `:active`.
*   `.animate-fade-in`: Fades element from 0 to 1 opacity over 0.5s.
*   `.animate-slide-up`: Element rises 14px while fading in over 0.5s.
*   `cursorBlink`: Animation available for blinking carets.
*   `scanSweep`: Panning animation for radar / scanning effects.
