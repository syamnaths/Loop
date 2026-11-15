---
name: modern-web-guidance
description: "Google Modern Web Guidance (web.dev). Enforces Core Web Vitals (LCP, INP, CLS), Baseline web platform features, progressive enhancement, semantic HTML, responsive layout, accessibility, and browser performance budgets for web-facing UIs."
---

# Modern Web Guidance (Google web.dev)

Based on Google's [web.dev](https://web.dev/) modern web platform guidance. Apply whenever building or reviewing web-facing UIs.

## 1. Core Web Vitals & Performance Budgets
- **LCP (Largest Contentful Paint <= 2.5s):** Prioritise critical hero/LCP assets (`fetchpriority="high"` when needed), avoid render-blocking scripts/CSS, and size images explicitly (`width`/`height` or `aspect-ratio`).
- **INP (Interaction to Next Paint <= 200ms):** Keep main-thread tasks short, avoid long synchronous work in event handlers, and give immediate visual feedback on user actions.
- **CLS (Cumulative Layout Shift <= 0.1):** Reserve space for async content, skeletons, fonts (`font-display: swap`), and media so elements never jump during load.

## 2. Web Platform & Progressive Enhancement
- **Semantic HTML first:** Use native `<button>`, `<a href>`, `<label>`, `<dialog>`, `<details>`, and landmark elements before reaching for ARIA workarounds or heavy JS wrappers.
- **Baseline web features:** Prefer standard, broadly supported CSS/DOM/Web APIs (CSS Grid/Subgrid, Flexbox, Container Queries, `:has()`, `prefers-reduced-motion`, native form validation) over unnecessary third-party packages.
- **Progressive enhancement & resilience:** Core navigation, forms, and content must work cleanly across network conditions, slow devices, and keyboard-only input.

## 3. Accessibility, Media & Privacy
- Meet WCAG AA contrast, visible `:focus-visible` rings, keyboard Tab order, and screen-reader labels.
- Use modern image formats (`AVIF`/`WebP` with fallbacks), responsive `srcset`/`sizes`, and lazy-loading (`loading="lazy"`) only for below-the-fold media (never on the LCP element).
- Minimise third-party scripts and trackers; keep CSP, HTTPS/secure headers, and cookie/consent rules aligned with `SECURITY.md` and `.loop/legal-checklist.md`.
