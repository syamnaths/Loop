---
name: astryx
description: "Astryx design system skill. Used when selected by the owner or chosen when the owner has not taken any design action after being asked with A/B/C options. Defines semantic token architecture, typography, 4pt/8pt spatial rhythm, component state completeness, and accessibility floors."
---

# Astryx Design System

Astryx is a structured, token-first design system available in Loop. It is **not** applied silently as an automatic default: when the owner has not supplied a `template-page/`, approved reference, or existing product system—and has not yet taken any action on design—**ask the owner first** with concise A/B/C options (with Astryx as an explicit option). Apply Astryx once the owner selects it or confirms no preference.

## 1. SOI Precedence
- **Owner reference / existing product system wins** (SOI: specific overrides general). Never silently redesign an existing product.
- **No silent default:** If the owner has taken no action on design, ask once in plain words (A: Astryx / B: Platform-native Material Design 3 or Apple HIG / C: Provide a reference or custom direction) before locking a design system.
- **Package rule:** Astryx is a design system, not a mandatory dependency. Reuse the project's existing stack; never install a UI library just to adopt Astryx.

## 2. Semantic Token Contract
Define and record these semantic tokens in the project design notes (`DESIGN.md` or `.loop/` design notes) before writing feature UI:
- **Surfaces:** `bg-canvas`, `bg-surface`, `bg-elevated`, `border-subtle`, `border-strong` (with full light/dark or theme parity when supported).
- **Content:** `text-primary`, `text-secondary`, `text-muted`, `text-inverse`.
- **Accents & Status:** `accent-primary`, `accent-hover`, `status-success`, `status-warning`, `status-danger`, `status-info` (no generic cliché purple/blue gradients).
- **Spatial Rhythm & Radii:** 4pt/8pt modular spacing scale (`4, 8, 12, 16, 24, 32, 48, 64`), consistent radius tokens (`sm`, `md`, `lg`, `pill`), and restrained elevation/shadow steps.

## 3. Typography & Hierarchy
- Pair a deliberate display/heading voice with a clean, legible body font and a monospace font for IDs, code, or tabular metrics (`font-variant-numeric: tabular-nums`).
- Keep readable line lengths, clear typographic scale contrast, and explicit line-height/tracking.

## 4. Component, Motion & Accessibility Floor
- **All states required:** Resting, hover, focus-visible, active/pressed, disabled (with reason/tooltip), loading (skeleton/spinner), empty (with clear CTA), error (calm, translated), and overflow/truncation (see `skills/web-design/SKILL.md` §7–8).
- **Motion:** Subtle purposeful transitions, hover/micro-interactions, and smooth loaders with keyboard/touch equivalents and `@media (prefers-reduced-motion: reduce)` fallbacks.
- **Accessibility:** WCAG AA contrast, 44×44px+ touch targets, visible unclipped keyboard focus rings, and zero cumulative layout shift.
- **No mixed systems:** Do not mix competing component aesthetics on the same screen. If the owner supplies a concrete Astryx token file or Figma spec, that spec overrides these baseline tokens.
