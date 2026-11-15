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
- **Placeholders & Helper Text:** Show expected formatting (e.g. date formats, password rules) inside or below inputs. Never rely on placeholder text alone as a field label—labels must remain visible.
- **Focus & Active States:** Highlight the currently selected input box clearly so keyboard and mobile users know where they are typing.
- **Inline Validation:** Show green checkmarks for valid entries and clear red error messages right below invalid fields. Validate after the user finishes typing (on blur/pause) rather than on every keystroke.
- **Disabled States:** Visually mute buttons or inputs that cannot be used yet and add a tooltip explaining what needs to happen to enable them.
- **Unsaved Changes Warning:** Trigger a confirmation popup if a user tries to close a tab or navigate away after editing a form.
- **Native Attributes:** Numeric inputs, date pickers, and masks should leverage appropriate HTML5 attributes (`inputmode`, `autocomplete`, `type`).

### 8. Complete Screen, System & Feedback States
Every user-facing feature must explicitly design and handle all applicable states below:

1. **Core Screen & Data States** (every page or component that fetches or displays data):
   - **Empty State:** Shown when a user has no data yet (e.g. empty cart, new dashboard); include a friendly explanation and a clear call-to-action to add the first item.
   - **Loading State (Skeletons & Spinners):** Use skeleton screens (gray placeholder shapes, CLS = 0) for page layouts and spinners for small actions like button clicks.
   - **Ideal State:** The standard view when data is loaded, populated, and functioning normally.
   - **Partial State:** Shown when only some data is available (e.g. incomplete user profile); gently prompt the user to fill in the missing pieces.
   - **Overflow / Max State:** Shown when content exceeds normal limits (e.g. very long usernames, 100+ notifications); use text truncation (ellipses) and pagination or infinite scroll to prevent broken layouts.
2. **Error & System Pages:**
   - **404 Not Found:** Include a search bar, popular links, or a button to go back home.
   - **500 Server Error:** Apologize briefly, reassure the user their data is safe, and provide a "Try Again" button.
   - **403 Forbidden / Unauthorized:** Explain why access is restricted and offer a login prompt or a way to request access.
   - **Offline / No Internet Connection:** Display a clear banner, allow viewing cached content if possible, and auto-retry when the connection returns.
   - **Maintenance Mode:** State when the service will be back online and offer a status page link.
   - **Session Timeout:** Save any unsaved work locally if possible and provide a quick re-login modal.
3. **Feedback & Micro-Interactions:**
   - **Toast Notifications / Snackbars:** Brief popups confirming background actions (e.g. "Message sent", "Item deleted"); include an "Undo" button for destructive actions.
   - **Confirmation Modals:** Ask for explicit confirmation before permanent actions (e.g. deleting an account, canceling a subscription).
   - **Progress Indicators:** Show step-by-step progress bars for multi-page checkouts, onboarding flows, or file uploads.
   - **Hover & Pressed States:** Provide subtle color or shadow changes when hovering over clickable elements or tapping buttons on mobile.
4. **First-Time & Accessibility States:**
   - **Onboarding / Walkthroughs:** Brief tooltips or welcome screens guiding new users through core features without overwhelming them.
   - **Search No Results:** Suggest spelling corrections, broader keywords, or popular categories when a search query returns zero matches.
   - **Keyboard Navigation & Focus Rings:** Ensure every interactive element can be reached using the `Tab` key with a visible outline around the focused item.
   - **Image Fallbacks:** Display a default avatar or broken-image icon if a user-uploaded photo fails to load.

### 9. Visual Proof & Self-Audit Checklist
Before declaring any front-end UI delivered or complete:
- [ ] Did I inspect the rendered output across mobile (375px), tablet (768px), and desktop (1280px+)?
- [ ] Is there zero horizontal scroll overflow, and are long values/lists handled with truncation and pagination or infinite scroll?
- [ ] Are all font sizes, weights, and colors pulled from a coherent token system?
- [ ] Do all buttons, links, and inputs have hover, focus-visible, active/pressed, and disabled-with-tooltip states?
- [ ] Is contrast verified for text against its direct background?
- [ ] Does keyboard navigation (`Tab`, `Enter`, `Escape`) work seamlessly with visible focus rings?
- [ ] Are all 5 core data states (empty, loading skeletons/spinners, ideal, partial, overflow), system/error pages (404, 500, 403, offline, maintenance, session timeout), form states (helper text, post-typing inline validation, unsaved changes warning), feedback states (toasts with undo, confirmation modals, progress indicators), and first-time/fallback states (onboarding, search no results, image fallbacks) handled where applicable?
