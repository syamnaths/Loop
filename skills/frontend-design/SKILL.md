---
name: frontend-design
description: "Anthropic-style frontend design skill. Prevents generic AI slop, bland layouts, and predictable styling. Enforces design-lead planning, bold typography pairings, cohesive 4-6 color palettes, intentional spatial asymmetry, microcopy standards, and self-critique before code generation."
---

# Frontend Design (Anthropic-Style)

Based on [anthropics/skills - frontend-design](https://github.com/anthropics/skills/blob/main/skills/frontend-design/SKILL.md).

This skill guides the agent to act as an opinionated design lead at a boutique studio rather than a generic code generator, eliminating AI design clichés ("AI slop") before writing HTML, CSS, or component code.

## 1. The Design Lead Mindset
- Never generate generic, template-driven interfaces (no default purple/blue gradients on plain white backgrounds, no centered headers with floating badge pills and 3 identical icon cards).
- Every project has a distinct aesthetic personality: decide on a tailored design direction (e.g. bold editorial, technical instrument, brutalist, warm organic, or high-end luxury) matched to the domain.
- Commit to purposeful creative risk: asymmetric balance, bold scale contrasts, custom border treatments, or dramatic typographic focus.

## 2. Pre-Code Design Plan (Mandatory Step)
Before writing frontend code, specify:
1. **Subject & Target User:** What job does this screen do, and who is looking at it?
2. **Color Palette (4–6 hex values):**
   - Background canvas (base)
   - Surface/Card elevation
   - High-contrast text/content primary
   - Muted secondary/caption
   - Distinctive brand accent (never default `#6366f1` / `#3b82f6` unless requested)
   - Border/divider tone
3. **Typography Pairings:** Distinct display/headline font paired with a clean, readable body typeface. Define explicit tracking (letter-spacing) and leading (line-height).
4. **Layout & Spatial Concept:** Wireframe the composition. Avoid symmetric repetitive grids; introduce hero variation, off-center focal points, or modular bento sizing.
5. **Self-Critique:** Review the plan against common AI tropes: "Does this look like an instant AI template, or does it feel custom-designed by a human design director?"

## 3. Microcopy & Content
- Microcopy is visual design: avoid placeholder gibberish ("Lorem Ipsum"), broken text labels, or robotic button labels ("Submit", "Click Here").
- Use active, contextual labels ("Explore atlas", "Export telemetry", "Save and continue").
- Design for content variance: long translated German names, empty lists, multi-line titles, and truncated paths.

## 4. Production Quality Floor
- Strict responsive fidelity: perfect display on mobile (375px), tablet, and desktop viewports.
- Keyboard navigation: visible, offset focus rings that never get clipped by `overflow: hidden`.
- Motion: purposeful entrance transitions with natural curves; instant zero-movement fallback on `@media (prefers-reduced-motion: reduce)`.
