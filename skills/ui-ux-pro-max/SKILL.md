---
name: ui-ux-pro-max
description: "UI/UX Pro Max intelligence skill based on nextlevelbuilder/ui-ux-pro-max-skill. Enforces structured design reasoning, industry-tailored color/typography profiles, 50+ UI genre styles (Bento Grid, Brutalism, Glassmorphism, Clean SaaS, Dark Mode, High-Density Dashboard), and comprehensive UX guidelines."
---

# UI/UX Pro Max Intelligence Skill

Based on [nextlevelbuilder/ui-ux-pro-max-skill](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill).

UI/UX Pro Max equips the agent with systematic design intelligence, genre-specific visual frameworks, and rigorous usability guidelines to select the right design system for each product type.

## 1. Domain & Genre Matching
Do not apply generic styling across diverse products. Match the visual genre to the domain:
- **Developer Tools / Technical Products:** High-density, monospaced accents, dark mode first, keyboard shortcut indicators (`⌘K`), subtle borders, terminal/code-block emphasis.
- **B2B SaaS / Productivity:** Clean, spacious, neutral slate/zinc canvas, crisp typography, subtle tonal elevations, high-contrast primary actions.
- **Consumer / Editorial / Brand:** Typographic drama (serif/display headers paired with modern sans-serif body), intentional whitespace, warm tones, rich editorial photography/imagery.
- **Fintech / Data Dashboards:** High-density bento grids, tabular numbers (`font-variant-numeric: tabular-nums`), green/red semantic indicators with accessible secondary cues (icons/text labels, not color alone), compact chart cards.

## 2. Genre Architectures (50+ Style Palette)
Select and execute proven UI paradigms:
- **Bento Grid:** Modular, asymmetric card layouts grouping related features into cohesive tiles with distinct visual weights.
- **Subtle Glassmorphism:** Restrained backdrop blur (`backdrop-filter: blur(12px)`) with hairline translucent borders (`rgba(255,255,255,0.1)`) on dark surfaces.
- **Modern Minimalist / Linear-Style:** Dark mode canvas, 1px borders, subtle hover highlights, buttery micro-interactions, uncluttered headers.
- **Neo-Brutalist / Editorial:** Bold geometric borders (2px solid black), high-contrast blocks, hard shadow offsets (`box-shadow: 4px 4px 0px #000`), sans-serif typography.

## 3. Usability, Interaction & UX Invariants
- **Fitts's Law:** Ensure primary targets are large and accessible; touch targets are minimum 44×44px on touch devices.
- **Hick's Law:** Minimize cognitive overload; progressive disclosure for complex configuration forms.
- **Zero CLS (Cumulative Layout Shift):** Always reserve space for dynamic content, images, and charts using aspect ratios and skeleton placeholders.
- **Accessibility Invariants (WCAG AA):**
  - Minimum 4.5:1 contrast ratio for standard text; 3:1 for large text and UI components.
  - Never convey state or status using color alone (pair with icons, text, or patterns).
  - Explicit ARIA labels on icon-only buttons.
  - Fully functional keyboard focus trapping in modal dialogs and drawers.
