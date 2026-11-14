---
name: impeccable
description: "Impeccable frontend craft, critique, and anti-pattern detection skill based on pbakaus/impeccable. Provides structured design dials (bolder, quieter, distill, typeset, polish, audit), context persistence (PRODUCT.md / DESIGN.md), and automated critique loops to eliminate AI design flaws."
---

# Impeccable Frontend Craft & Critique

Based on [pbakaus/impeccable](https://github.com/pbakaus/impeccable).

Impeccable bridges the gap between raw AI code generation and impeccable craftsmanship. It provides design vocabulary, context files, and structured critique workflows to steer interfaces from functional to world-class.

## 1. Design Steering Vocabulary & Dials
When iterating on UI or receiving feedback, apply specific design dials:
- **`bolder`**: Increase contrast, enlarge headline scales, intensify key accent colors, and amplify physical presence.
- **`quieter`**: Soften aggressive contrasts, reduce visual noise, tone down secondary elements, and expand whitespace.
- **`distill`**: Strip non-essential cards, dividers, decorations, and redundant badges. Focus entirely on the primary action and data.
- **`colorize`**: Replace monotonous monochrome/grey palettes with an intentional, cohesive color scheme with emotional depth.
- **`typeset`**: Perfect typographic hierarchy, measure (45–75 characters per line), vertical baseline rhythm, optical alignment, and tracking.
- **`polish`**: Smooth out border radii, optical alignment, padding inconsistencies, hover transitions, and focus rings.
- **`audit`**: Run mechanical quality checks against accessibility (contrast, labels), layout shifts (CLS), touch targets (44px+), and responsive overflows.

## 2. Design System Context
Capture and preserve design tokens in project documents (`DESIGN.md` or `.loop/platform.md` design tokens):
- Semantic color variables (`--bg`, `--surface`, `--text`, `--muted`, `--accent`, `--border`).
- Elevation levels (tonal layering and subtle 1px border highlights over heavy fuzzy drop shadows).
- Spacing modular grid (4px/8px increments).
- Radius scale (e.g. `--radius-sm: 4px; --radius-md: 8px; --radius-lg: 12px;`).

## 3. Impeccable Critique Loop
Before approving or delivering any user-facing screen:
1. **Layout & Density:** Is the screen cluttered? Is the information hierarchy immediate within 3 seconds of scanning?
2. **Typography Check:** Are headings commanding? Is body text comfortable to read without straining?
3. **Affordance & States:** Does every interactive element clearly signal that it is clickable? Are hover, active, and focus states clearly distinguished?
4. **Mechanical Anti-Pattern Check:**
   - No nested cards-inside-cards without semantic purpose.
   - No generic centered floating badge pills ("✨ AI Powered ✨").
   - No clipping or horizontal overflow on small screens.
   - No unstyled browser default form controls.
