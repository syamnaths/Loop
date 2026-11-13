---
name: web-design
description: "Web and front-end designer skill for Loop. Use when creating, styling, refining, or reviewing user interfaces. Enforces thinking like a professional front-end designer rather than a raw code generator: visual hierarchy, typography scale, semantic color systems, intentional whitespace, states, micro-interactions, responsive composition, accessibility, and bespoke visual polish."
---

# Web Design & Front-End Designer Skill

This skill guides the AI to design and build user interfaces with the craft, aesthetic judgment, and user empathy of an experienced front-end designer rather than a mechanical code generator.

## Core Mindset: Designer vs Code Generator

| A Code Generator... | A Front-End Designer... |
|---|---|
| Dumps unstyled inputs and default buttons onto a grid | Curates visual hierarchy, rhythm, and eye-flow before writing markup |
| Uses raw hex codes or random Tailwind utilities (`bg-blue-500`, `p-4`) | Defines and adheres to a cohesive design token system (semantic colors, type scales, modular spacing) |
| Designs only the happy path | Designs all states: initial, loading, empty, focused, hover, active, error, success, validation |
| Adds generic grey cards with sharp drop shadows | Sculpts subtle elevation, tonal layering, tactile borders, and atmospheric depth |
| Uses generic placeholder text and unconsidered line lengths | Shapes typography for readability: line heights, measure (45–75 chars), font pairing, letter spacing |
| Creates stiff, instant snap transitions | Crafts purposeful micro-interactions, spring transitions, and reduced-motion fallbacks |
| Shrinks a desktop layout until it breaks on mobile | Composes mobile-first, responsive layouts tailored to human thumb zones and screen ergonomics |

---

## The 8 Principles of Front-End Craft

### 1. Typography & Hierarchy
- **Type Scale:** Establish a harmonic scale (e.g., 1.250 Major Third or 1.333 Perfect Fourth) for `display`, `h1`–`h4`, `body-large`, `body`, `caption`, and `overline`.
- **Readability & Measure:** Never let body copy stretch edge-to-edge. Restrict text measure to 45–75 characters per line (`max-w-prose` or `65ch`).
- **Vertical Rhythm:** Match line height (`line-height: 1.5–1.7` for body, `1.1–1.25` for headers) and maintain consistent paragraph spacing.
- **Contrast & Weight:** Do not rely solely on font size for hierarchy; pair font weight, letter spacing (tracking), and color value to guide the eye.

### 2. Semantic Color & Atmospheric Depth
- **Semantic Tokens:** Avoid arbitrary color values. Use tokens: `surface-base`, `surface-elevated`, `surface-sunken`, `content-primary`, `content-muted`, `border-subtle`, `primary-interactive`, `danger-surface`, etc.
- **Layering Over Heavy Shadows:** Build depth using surface tinting and light borders (`1px solid rgba(255,255,255,0.08)` or subtle slate borders) rather than heavy, dirty drop shadows.
- **Accessible Contrast:** Verify WCAG AA (4.5:1 for normal text, 3:1 for large text) across light and dark modes.

### 3. Spacing, Rhythm & Composition
- **Consistent Grid/Scale:** Base spacing on an 8pt (or 4pt) system: `4px`, `8px`, `12px`, `16px`, `24px`, `32px`, `48px`, `64px`.
- **Intentional Whitespace:** Whitespace is not empty space—it separates ideas, provides breathing room, and gives premium character to interfaces.
- **Content-Driven Containers:** Align elements to optical centers and consistent baseline grids. Group related items closely (Gestalt principle of proximity).

### 4. Interactive States & Tactile Feedback
Every interactive element must express clear states:
1. **Resting / Default:** Inviting, clear affordance (looks clickable/interactive).
2. **Hover:** Subtle elevation, background tint, or border highlight (`150ms–200ms ease-out`).
3. **Focus-Visible:** Accessible, high-contrast focus rings (`outline: 2px solid var(--accent); outline-offset: 2px;`) that never clip.
4. **Active / Pressed:** Physical feedback (e.g. `transform: scale(0.98)` or inset shadow).
5. **Loading / Pending:** Skeleton screens or inline spinners without layout shifts (CLS = 0).
6. **Disabled:** Distinct opacity with `cursor: not-allowed` and appropriate ARIA attributes.
7. **Empty:** Thoughtfully designed empty states with reassuring copy, an illustration/icon, and a clear call-to-action.

### 5. Motion & Delight
- **Purposeful:** Motion should clarify cause and effect (e.g. expanding an accordion pushes adjacent content smoothly).
- **Duration & Easing:** Snappy transitions (`150ms–300ms`) using natural curves (`cubic-bezier(0.16, 1, 0.3, 1)` or standard ease-out). Avoid long, sluggish animations.
- **Respect Preferences:** Always support `@media (prefers-reduced-motion: reduce)` by removing spatial movement and keeping instantaneous or cross-fade state changes.

### 6. Responsive Ergonomics & Layout
- **Mobile First:** Ensure minimum touch target sizes of 44×44px (or 48×48px) for buttons, tabs, and form elements.
- **Thumb Zone Navigation:** Place primary mobile actions within easy reach of one-handed thumb navigation.
- **Fluid Layouts:** Use CSS Grid and Flexbox with `clamp()`, `minmax()`, and modern container queries rather than brittle hardcoded pixel widths.

### 7. Form Craft & Input Design
- Labels must remain visible (avoid placeholder-only forms).
- Inputs should have clear border states on focus and real-time inline validation with helpful, human messages.
- Numeric inputs, date pickers, and masks should leverage appropriate HTML5 attributes (`inputmode`, `autocomplete`, `type`).

### 8. Visual Proof & Self-Audit Checklist
Before declaring any front-end UI delivered or complete:
- [ ] Did I inspect the rendered output across mobile (375px), tablet (768px), and desktop (1280px+)?
- [ ] Is there zero horizontal scroll overflow?
- [ ] Are all font sizes, weights, and colors pulled from a coherent token system?
- [ ] Do all buttons, links, and inputs have hover, focus, and active states?
- [ ] Is contrast verified for text against its direct background?
- [ ] Does keyboard navigation (`Tab`, `Enter`, `Escape`) work seamlessly?
- [ ] Are empty states and error boundaries visually handled?
