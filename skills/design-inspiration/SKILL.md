---
name: design-inspiration
description: "Design reference, virtual moodboard, and multi-device verification skill incorporating Awwwards-MCP, InspoMCP, and Responsively App. Enforces gathering real-world design DNA, building a virtual moodboard, targeting 99.9% fidelity to the moodboard, and testing multi-viewport responsive parity."
---

# Design Inspiration, Moodboard & Multi-Device Verification

Integrates reference discovery and verification tools:
- **Awwwards-MCP** ([INSANE0777/Awwwards-mcp](https://github.com/INSANE0777/Awwwards-mcp)): Extract design DNA, tokens, structural band maps, and motion metadata from award-winning websites.
- **InspoMCP** ([inspomcp.dev](https://inspomcp.dev)): Search curated production archives for desktop/mobile screenshots, font ramps, and real production design systems.
- **Responsively App** ([responsively-org/responsively-app](https://github.com/responsively-org/responsively-app)): Multi-device mirrored viewport testing and automated agent-driven responsive verification.

## 1. Trigger Conditions
Activate this skill:
- **Project Start / Discovery:** When designing the initial screen, template page (`design/template-page/`), or establishing the visual direction.
- **New Feature / UI Screen Map:** When picking the next planned map (`cmdNext`) that introduces user-facing UI or layout changes.
- **Responsive Inspection Gate:** Before flipping a UI map to `delivered`, verify across mirrored mobile/tablet/desktop viewports.

## 2. Step 1: Inspiration & Virtual Moodboard Creation
When starting design work, do not design in a vacuum:
1. **Query Reference Tools:**
   - Use **InspoMCP** (`inspomcp.dev`) and **Awwwards-MCP** (`INSANE0777/Awwwards-mcp`) to retrieve real-world design references matching the product domain (SaaS, FinTech, DevTools, E-commerce, Media).
   - Extract real color palettes, typography pairings, layout hierarchies, and motion dynamics.
2. **Synthesize the Virtual Moodboard:**
   - Define the visual concept in project design notes (`DESIGN.md` or `.loop/tracks/<map-id>/spec.md`):
     - Aesthetic Genre & Tone (e.g. Minimalist Linear-Style, Bento Grid, High-Density Technical, Editorial Serif).
     - Palette tokens (4–6 hex values).
     - Font pairings & scale.
     - Focal anchor (asymmetric hero, data widget, or tactile card structure).
3. **The 99.9% Fidelity Target:**
   - **Crucial Invariant:** Always target the final implementation to achieve **99.9% visual and architectural fidelity** to the synthesized moodboard / reference.
   - Do not cut corners or let standard UI defaults water down the agreed aesthetic direction.

## 3. Step 2: Multi-Device Responsive Verification
Before claiming any UI is verified:
- Use **Responsively App** (or headless Playwright viewports) to inspect simultaneous rendering across:
  - Mobile (375px / 414px) — thumb zones, minimum 44×44px touch targets.
  - Tablet (768px / 834px) — adaptive grid collapse without text overflow.
  - Desktop (1280px / 1440px+) — container constraints (`max-w-*`), optical alignment, zero horizontal scrollbar.
- Verify mirrored interaction fidelity (clicking, scrolling, form entry).
