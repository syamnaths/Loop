# {{name}} — working agreement

This project uses **Loop** (atlas-first). These rules apply to every session, agent and contributor.

- **Platform:** {{platform}} (chosen at the start; details in `.loop/platform.md`)
- **Stack:** {{stack}}

## Automatic pickup

At the start of a session, after context compaction or when resuming:

1. Read the `CURRENT RESUME` block at the top of `HANDOFF.md`. It is the active checkpoint; older entries are history.
2. Read `.loop/platform.md`, `Loop/loop.md`, `Loop/ATLAS-FIRST.md`, `Loop/OWNER-COMMUNICATION.md` and `Loop/EFFICIENT-WORKFLOW.md`. Load other Loop files only when relevant.
3. Run `{{cmdStatus}}`. It shows delivered / building / planned maps, the next map to build and any drift.
4. Verify the branch, working tree and relevant source before trusting recorded status.
5. Continue the recorded next action within the owner's authorisation, unless the newest request changes it. Do not restart finished work or ask the owner to repeat known requirements.
6. Before handing off, update the same `CURRENT RESUME` block. Do not create competing status files.

## Goal continuity

**Goal pauses belong to the owner.** Keep the goal active until it is complete. Never set it to paused unless the owner explicitly asks. Take necessary temporary rests (for example cooldowns, rate-limit waits or required recovery) without pausing the goal; record the reason and restart condition, then continue automatically when checks pass and the host permits. Continue other authorised work when safe. A rest never bypasses resource guards, approval gates or host limits. The owner may pause while riding or travelling and resume on arrival; do not infer a pause from absence or travel, and do not resume an owner-paused goal until the owner asks.

## Prioritise before starting work

Keep one active delivery map (the current big rock). Finish its supporting fixes, tests and docs before unrelated work. Dependencies come first; then the smallest valuable outcome and risk reduction. `meta.buildOrder` is the agreed order; the Eisenhower matrix is triage, not an automatic override. Record blockers and reasons for reordering. Before switching from a blocked active map, checkpoint its restart step in the track and handoff and return it to `planned` with `blockedBy` retained. Multiple building maps are invalid; priority never bypasses dependencies or release boundaries. See `Loop/ATLAS-FIRST.md` → Priorities and one active big rock.

## Build from the atlas

`docs/app-map/` is the shared picture of the product. Every feature addition, removal or behaviour change updates its map in the same change.

- Pick work with `{{cmdNext}}`. Make the map exact before coding; set it to `building`.
- Build to the map. Add behaviour tests. Then add `source` references (`file:line`) and set the map to `delivered`.
- Run `{{cmdAtlas}}` after every map change (it refuses broken edges and missing source) and `{{cmdCheck}}` before each commit. Run `{{cmdVerify}}` for structural or visual atlas changes.
- Product tests: `{{projectTest}}`. Prove each feature at the strongest level listed in `.loop/platform.md` and say which level you reached.
- Plans go to `planned` maps or `docs/app-map/FIX-QUEUE.md`, never into delivered maps.
- Each feature has a track in `.loop/tracks/<map-id>/spec.md`. Keep its checklist current.

{{templateRule}}## Talk to the owner

{{ownerStyle}}

Give approve-style options (A recommended / B / C) only for decisions that change the result. Do routine work yourself. Show proof the owner can judge: {{visualProof}}. Say what is verified and what is not.

## Professional design before delivery

**Think like a front-end designer, not a code generator.** When building or reviewing user interfaces, adopt a front-end designer's craft rather than generating mechanical markup or raw utility soup. Apply the integrated design skills:
- **Reference Gathering, Moodboards & 99.9% Target:** Follow `Loop/skills/design-inspiration/SKILL.md` ([Awwwards-MCP](https://github.com/INSANE0777/Awwwards-mcp), [InspoMCP](https://inspomcp.dev), [Responsively App](https://github.com/responsively-org/responsively-app))—query real design references, build a virtual moodboard with exact tokens, and target 99.9% fidelity to that moodboard.
- **AI Slop & Cliché Detection:** Follow `Loop/skills/ai-slop-detector/SKILL.md` ([AI Slop Detector](https://github.com/flamehaven01/ai-slop-detector))—audit code and visuals for artificial superficiality, cliché purple gradients, floating pills, empty stubs, and phantom imports before delivery.
- **Design Lead Planning & Anti-Slop:** Follow `Loop/skills/frontend-design/SKILL.md` ([Anthropic Frontend Design](https://github.com/anthropics/skills/blob/main/skills/frontend-design/SKILL.md))—plan 4–6 specific hex colors, bold typography pairings, and layout concepts with deliberate character before coding; eliminate generic AI tropes.
- **Frontend Craft & Critique Dials:** Follow `Loop/skills/impeccable/SKILL.md` ([Impeccable](https://github.com/pbakaus/impeccable))—use design dials (`bolder`, `quieter`, `distill`, `typeset`, `polish`, `audit`), enforce token consistency (`DESIGN.md`), and run mechanical anti-pattern audits.
- **UI/UX Intelligence & Genre Systems:** Follow `Loop/skills/ui-ux-pro-max/SKILL.md` ([UI/UX Pro Max](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill))—match domain aesthetics to proven genres (Bento Grid, High-Density Dashboards, Minimalist Linear-Style, Modern SaaS, Dark Mode) with WCAG AA accessibility, Fitts's law target sizing (44×44px+), and zero cumulative layout shifts.
- **Foundational Craft:** Follow `Loop/skills/web-design/SKILL.md` for responsive ergonomics, modular 8pt/4pt spacing scales, optical alignment, and complete state coverage (resting, hover, focus-visible, active, loading, empty, error).

**Design-system selection.** The owner's approved reference or existing product system takes precedence. Otherwise use [Material Design 3](https://m3.material.io/) as the default for web, Android and cross-platform interfaces, customised with the product's brand tokens. For native iOS/macOS use [Apple Human Interface Guidelines](https://developer.apple.com/design/human-interface-guidelines/) and native components. Other native platforms follow their platform conventions. These defaults authorise an initial representative screen, not a silent redesign of an existing product. Record the chosen system and tokens in the project design notes; obtain the owner's decision before a major new visual commitment. A design system is not a package: reuse the existing stack and check current supported implementations before proposing any new dependency. Avoid mixing competing component styles; verify accessibility and visual quality in the actual implementation.

Every user-facing feature must look and behave like a coherent finished product. Follow the owner's reference and the existing design system; reuse established components. Without a reference, propose a concise direction suited to the audience and platform, show one representative screen, and obtain the owner's decision on a major new visual direction before spreading it across the product. Routine polish within the agreed direction needs no repeated approval.

**Motion defaults.** Include hover effects, smooth loading indicators, 3D motion, entrance reveals, micro-interactions and parallax in the visual design, adapted to the product and platform. Use subtle, purposeful effects and provide touch and keyboard equivalents for hover. Respect reduced-motion settings by removing or replacing spatial motion, including 3D, reveals and parallax, while keeping status and feedback clear. Avoid delaying access to content, blocking interaction or adding unnecessary dependencies; verify performance and the reduced-motion experience on representative screens.

- Establish consistent typography, spacing, alignment, colour, iconography and component states. Use clear information hierarchy, readable content widths and restrained decoration; avoid generic ornament that distracts from the task.
- Design the full experience: loading, empty, success, error, validation, disabled and permission states where applicable. Use real approved content; do not ship placeholder copy, broken assets or dead controls.
- Adapt to the platform and relevant screen sizes, including long translated text. Check keyboard navigation, visible focus, labels, contrast, touch targets and reduced-motion preferences where relevant.
- Before delivery, inspect the rendered feature at representative sizes and exercise the key interactions. Correct clipping, overflow, inconsistent spacing and unclear actions; show the owner representative screenshots with any remaining limits. Source inspection alone is not visual proof. If rendering tools are unavailable, record visual review as blocked rather than claiming polish is verified.

## Product rules

- All user-facing text in every supported language at once ({{languages}}) in {{textHome}}, with placeholder checks in tests. Gender-neutral wording.
- {{versionRule}}
{{platformRules}}
- No raw developer text for users; calm translated messages, quiet technical logs.
- Measure before claiming sizes, speed or savings. Device feel and sound need a device check.
- Consent, privacy and safety first for sensitive features; never store private choices.

## Tests and security before delivery

Follow TDD for testable behavior: confirm a meaningful failing test before implementation, then GREEN and refactor. Reuse existing coverage; add unit tests for changed logic and integration tests for changed component boundaries, with failure paths where applicable. Record skipped or blocked levels honestly (details in Loop/DELIVERY-WORKFLOW.md). Before marking a feature delivered, perform the focused security review in Loop/SECURITY.md, list evidenced vulnerabilities and discuss them with the owner before remediation. Fix agreed findings, rerun tests and re-review. No findings means report limits and continue; no empty approval gate.

## Legal checklist

`.loop/legal-checklist.md` holds the 20 legal checks (rules in `Loop/LEGAL-CHECKLIST.md`). When a map collects personal data, adds cookies or trackers, a third-party API, a package, assets, AI content, payments, advice or marketing text, update those rows in the same change. The release needs check 20 (final legal audit) done. Loop drafts legal pages and flags lawyer items; the owner approves legal text before it is published. Never claim the product is legally compliant.

## Release boundary

Commit validated checkpoints locally. The owner approves every push to production, every deploy, every store release (see the `release` map) and every published legal page. If the agent cannot push, give one copy-paste command and confirm the remote afterwards.
