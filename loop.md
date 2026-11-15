# Loop — project collaboration policy

Loop is a local-first way to plan, build, check and hand over software with an AI agent and a human owner. Version 0.4 makes the **flow atlas** the centre of every project: new projects start from an atlas plan, and every feature is built to its map and closed by flipping that map to delivered. Loop is **platform-independent**: the platform (web, Android, iPhone, cross-platform mobile, desktop, backend, command-line, other, or several) is chosen by the owner or coder at the start and shapes the proof, rules and release steps. The method comes from the Lite meditation PWA, where it carried dozens of features across five languages without losing track.

## Companion files

| File | Use it for |
| --- | --- |
| [ATLAS-FIRST.md](./ATLAS-FIRST.md) | The atlas format and the build loop. Read for any feature work. |
| [OWNER-COMMUNICATION.md](./OWNER-COMMUNICATION.md) | How to talk to the owner: plain words, A/B/C options, honest status, release boundary. |
| [EFFICIENT-WORKFLOW.md](./EFFICIENT-WORKFLOW.md) | Bounded context, execution modes, routing evidence, cost honesty. |
| [DELIVERY-WORKFLOW.md](./DELIVERY-WORKFLOW.md) | Tracks, specs, reviews, debugging, release steps. |
| [SECURITY.md](./SECURITY.md) | Full security verification standard (OWASP-based). |
| [LEGAL-CHECKLIST.md](./LEGAL-CHECKLIST.md) | The 20 legal checks (privacy, terms, cookies, consent, user data rights, licences, assets, age, disclaimers, refunds, claims, final audit). Every project tracks them in `.loop/legal-checklist.md`. |
| [MODEL-ROUTING.md](./MODEL-ROUTING.md), [LOCAL-MODEL-ROUTING.md](./LOCAL-MODEL-ROUTING.md) | Optional model routing. Only when relevant. |
| [README.md](./README.md) | Starting a new project with `scripts/loop-init.mjs`. |

## 1. Activation

"Use Loop for this project", "Apply Loop" or "Resume with Loop" activates this policy. Loop is this local framework, not a product to look up online. Identify two roots: the **Loop root** (this folder) and the **target project root**. Never build the application inside the Loop root.

### New project (no product described yet)

Loop asks the questions, then starts building. The questions are the fields of [start/START.md](./start/START.md).

1. **Check the folder (read-only).** If it has a filled `START.md`, read it and ask only for what is missing or unclear. If it has a `template-page/` folder, that is the owner's basic template page.
2. **Ask once, in one message.** Short numbered questions in plain words: name; who it is for; what the first release must do; **which platform** (web, Android, iPhone, both mobile platforms, desktop, backend/API, command-line, other, or several); stack (or "to decide", plus whether installing the chosen stack's standard packages is pre-approved); languages and target user countries/regions (for legal checks); the features/pages with their steps; anything it must never do; and design direction ("Do you have a basic template page or reference? Otherwise choose: A) Astryx, B) platform-native Material 3 / Apple HIG, or C) custom"). If the owner is unsure about the platform or stack, give A/B/C options with a recommendation. Never pick the platform for the owner. Budgets, deadlines and limits come from the owner; never invent them. Before the answers, do not create files, initialise Git or install anything.
3. **Write the answers** into `START.md` in the target folder and put any template files in `template-page/` there.
4. **Start.** When the answers cover name, platform and at least one feature, do not wait for another approval: run `node <Loop>/scripts/loop-init.mjs <target> --git`. It reads `START.md`, moves the template page to `design/template-page/`, and creates the atlas plan, a release map for the platform, tracks, `.loop/platform.md`, handoff and an atlas check. Ask again only for answers that are missing or would change what gets built.
5. **Build straight away.** Show the atlas overview in one line, then run the build loop (ATLAS-FIRST.md) on the first map until it is delivered and proved. Report it with proof, then continue with the next map. Stop only at an approval gate (section 7) or an open product decision.

A coder who prefers the terminal can fill `START.md` by hand, or run `loop-init.mjs <target>` and answer the questions there; `--start` then hands over to the configured coding agent (`LOOP_AGENT`, for example `claude`, `codex`, `gemini`, `agy`) with "Use Loop for this project. Build the next atlas map."

### Existing project

Do not restart discovery. Read the newest request, `AGENTS.md`, the `CURRENT RESUME` block in `HANDOFF.md`, the affected atlas maps and the relevant source and tests. Verify the branch, working tree and recorded status against the real files. Continue the recorded next action within existing authorisation. If the project has no atlas, adopt it (`loop-init.mjs <project> --adopt`) and map current behaviour before adding features.

## 2. Clarity and decisions

- Do not act on an instruction whose meaning, target or result is unclear when guessing could change the work. Harmless typos may be read from clear context.
- The owner decides product direction, priorities, spending, names, publication and major architecture. Loop gives facts, risks and a recommendation, and records the decision (`APPROVED`, `APPROVED_WITH_CHANGES`, `DEFERRED`, `REJECTED`, `BLOCKED`).
- Ask only when the answer changes what gets built. Routine choices are Loop's job; say what was chosen.
- A withdrawn instruction is dropped completely.

## 3. Rule resolution, execution order, and checkpoint loop

### Rule resolution (Sūtra 1.4.2 — SOI vs. DOI)

When multiple Loop rules or skills fire at the same time, resolve collisions structurally—never by "later in the document" or ad-hoc patches:

- **Same Operand Interaction (SOI — *utsarga* vs. *apavāda*):** When two rules target the **same operand** (e.g., UI design system, active map, or routing target), the **more specific rule** always wins over the general default (owner's `template-page/` or existing product > platform default; `.loop/platform.md` > generic rule; `[LOOP_ROUTED_CHILD]` > parent routing; `meta.buildOrder` and `blockedBy` > ad-hoc urgency).
- **Different Operand Interaction (DOI — *vipratiṣedha*, *paraṃ* = right-hand side):** When two rules trigger simultaneously on **different operands** — **left = base** (atlas map, track, source, spec) vs. **right = suffix/attachment** (UI polish, legal rows, security review, routed child, handoff) — the **right-hand attachment resolves on its own operand first** without prematurely mutating or blocking the left base, and then merges into the closed state.

### Canonical execution order & operand trigger attachment

1. **Read state (Hot memory):** `HANDOFF.md` (`CURRENT RESUME`), `.loop/platform.md`, and `atlas-status --next` (never load Cold `archive/` or `handoff-archive/` unless investigating history).
2. **Lock the left base:** Select the single dependency-ready map (`meta.buildOrder`), confirm its steps, and move `planned` → `building` in `docs/app-map/atlas-data.mjs`. Never trigger domain skills before knowing the active map and its operands.
3. **Resolve SOI & attach right-side triggers by operand:**
   | Operand touched | Attached trigger (resolves on its operand before closing the base) |
   | --- | --- |
   | **UI / Visual** | `skills/design-inspiration/` → `skills/frontend-design/`, `skills/impeccable/`, `skills/ui-ux-pro-max/`, `skills/web-design/`, `skills/modern-web-guidance/` (web), `skills/astryx/` (when chosen) → `skills/ai-slop-detector/` |
   | **Data / Auth / API / Payment / Asset** | Matching rows in `.loop/legal-checklist.md` ([LEGAL-CHECKLIST.md](./LEGAL-CHECKLIST.md)) |
   | **Feature delivery** | Focused security review ([SECURITY.md](./SECURITY.md)) before `delivered` |
   | **High-risk / Bounded offload** | Cheapest safe execution mode ([EFFICIENT-WORKFLOW.md](./EFFICIENT-WORKFLOW.md) & [MODEL-ROUTING.md](./MODEL-ROUTING.md)) |
   | **Pause / Switch / Milestone** | Update `CURRENT RESUME` in `HANDOFF.md` in place (section 9) |
4. **TDD & smallest coherent change:** Confirm RED, implement GREEN, refactor. For bugs: reproduce, test one hypothesis at a time; after three failed hypotheses, stop and question the assumptions.
5. **Verify & review in order:** Run proportionate checks (unit + integration + visual screenshots at platform sizes). Run `SPEC_COMPLIANCE` before `QUALITY_AND_RISK` / security review.
6. **Merge & close the base (Tripādī one-way finalization, `8.2.1`):** Finalization runs strictly one-way (`SPEC_COMPLIANCE` → `QUALITY_AND_RISK` / `SECURITY.md` → `delivered` with real `file:line` references → atlas check → track, `FIX-QUEUE.md`, `HANDOFF.md` `CURRENT RESUME`, version/cache bumps → commit). Minor polish discovered in finalization goes to `FIX-QUEUE.md` instead of re-triggering earlier design/discovery loops; only critical/high blockers reopen the base.
7. **Continuous page & major-feature flow (no micro-stops):** Do not stop after tiny sub-steps, routine boilerplate, pre-approved stack package installs, or routine low/medium fixes. Keep building continuously across related sub-steps until a cohesive **page or major feature** is complete and proved, then report to the owner in plain words with what is verified, evidence level, and what is not. Stop mid-feature only at true approval gates (section 7) or unresolved critical/high blockers.

### Agent calling order & triggers

- **Trigger:** Stay `direct` when the current agent meets capability and context bounds. Dispatch a bounded child (`[LOOP_ROUTED_CHILD]`) or isolated specialist only when a task has distinct ownership, needs a different capability/context tier, or is a high-risk/parallel review. Never spawn recursive dispatches from a child, and never spin up a fleet for a one-file change.
- **Calling order:** **Coordinator** (owns state, atlas, handoff, integration) → **Bounded Worker** (isolated diff/task) → **Reviewers** (`SPEC_COMPLIANCE`, then `QUALITY_AND_RISK` / `SECURITY` / `ai-slop-detector`) → **Coordinator Integration** (verifies actual diff and test output before closing). If automatic dispatch is unavailable, fall back to `AWAITING_HUMAN_MODEL_SWITCH`.

### Craft rules for every change

- **Say your assumption.** When you go ahead on a reasonable reading, state the assumption in one line. When two readings would build different things, ask first (section 2).
- **Simplest thing that works.** No features, options, abstractions or error handling for cases that cannot happen unless the task needs them. If the change could be much shorter, make it shorter. Before writing new code, stop at the first step that fits:
  1. Is it needed now? If not, skip it and say so in one line.
  2. Does the language's standard library do it?
  3. Does the platform do it natively (a built-in input, a database rule, an OS setting)?
  4. Does a package the project already has do it? Add a new package only with a reason (approval gate when it needs the network).
  5. Only then write the smallest code that works.
- **Never trim the safety net.** Simplicity never removes input checks at trust boundaries, error handling that prevents data loss, security, accessibility or privacy protections.
- **Mark deliberate shortcuts.** When you knowingly take a simpler route with a limit, leave a short code comment starting `Known limit:` and add a line to `FIX-QUEUE.md`, so it is found later.
- **Closest-match fallback (*Sthāne 'ntaratamaḥ* `1.1.50`) & literal-vs-meta (*Svaṃ rūpam* `1.1.68`):** When multiple valid options fit, choose the closest match to the existing stack, platform, and capability tier. Never confuse a project's literal domain term with an internal Loop keyword.
- **Minimal vs. full replacement (`1.1.52`–`1.1.55`):** Default to surgical boundary edits (`alo 'ntyasya`); replace a whole module (`sarvasya`) only when multi-part structural change is required and approved.
- **Suppressed attachments (`na lumatā 'ṅgasya` `1.1.63`):** When a gate or operand is `n/a` or omitted for the platform (e.g., no UI in a CLI project), skip its dependent downstream transforms rather than forcing inapplicable checks.
- **Surgical edits & contract-preserving substitution (*Sthānivat* `1.1.56`):** Before removing or changing odd-looking code, find out why it exists (history, tests, map notes); remove it only when the reason is gone. Touch only the lines the task needs. Do not reformat, rename or refactor nearby code. When replacing a module or adapter, preserve its external contract, tests and atlas edges unless a breaking change is approved. Note other problems in `FIX-QUEUE.md` instead of fixing them on the side.
- **Clean removal (*Lopa* `1.1.60` / `1.1.62`):** Removing dead code or a feature means clean deletion (no commented-out stubs), plus reconciling any downstream callers, tests, locale keys, and atlas edges.
- **Strip internal markers (*It-lopa* `1.3.9`):** Internal orchestration tags (`[LOOP_ROUTED_CHILD]`, `[LOOP_CLASSIFY]`, internal track notes, debug scaffolds) guide execution and must never leak into user-facing UI, copy, or release bundles.
- **Seam & compatibility checks (*Samartha* `2.1.1` & *Sandhi*):** Verify contract/type compatibility before merging any isolated branch or subagent diff, and check integration seams (API schemas, i18n keys/placeholders, version/cache pins).
- **Check the real docs.** For an API, package or platform feature you are not sure about, read its current official documentation or the installed version's source; do not code from memory.
- **Done means a check passes.** Before coding, turn the task into a check (a test, a command or a screenshot) that fails or is missing now and will pass when the work is right. Loop until it passes.

## Prioritise before starting work

Keep one active delivery map (the current big rock). Finish its supporting fixes, tests and docs before unrelated work. Dependencies come first; then the smallest valuable outcome and risk reduction. `meta.buildOrder` is the agreed order; the Eisenhower matrix is triage, not an automatic override. Record blockers and reasons for reordering. Before switching from a blocked active map, checkpoint its restart step in the track and handoff and return it to `planned` with `blockedBy` retained. Multiple building maps are invalid; priority never bypasses dependencies or release boundaries. See `ATLAS-FIRST.md` → Priorities and one active big rock.

## Tests and security before delivery

Follow TDD for testable behavior: confirm a meaningful failing test before implementation, then GREEN and refactor. Reuse existing coverage; add unit tests for changed logic and integration tests for changed component boundaries, with failure paths where applicable. Record skipped or blocked levels honestly (details in DELIVERY-WORKFLOW.md). Before marking a feature delivered, perform the focused security review in SECURITY.md: auto-fix routine/low/medium vulnerabilities directly, rerun tests and re-review; stop to discuss with the owner only for critical/high architectural or breaking security trade-offs. No findings means report limits and continue; no empty approval gate.

## Professional design before delivery

**Think like a designer, not a code generator.** When building or reviewing user interfaces, adopt a front-end designer's craft rather than generating mechanical markup or raw utility soup. Follow the integrated design skills:
- **Reference Gathering, Moodboards & 99.9% Target:** Apply `skills/design-inspiration/SKILL.md` ([Awwwards-MCP](https://github.com/INSANE0777/Awwwards-mcp), [InspoMCP](https://inspomcp.dev), [Responsively App](https://github.com/responsively-org/responsively-app))—gather real-world design inspiration, construct a virtual moodboard with exact tokens, and target 99.9% fidelity to that moodboard across all viewports.
- **AI Slop & Cliché Detection:** Apply `skills/ai-slop-detector/SKILL.md` ([AI Slop Detector](https://github.com/flamehaven01/ai-slop-detector))—audit code and visuals for artificial superficiality, cliché purple gradients, floating pills, empty stubs, and phantom imports before marking work complete.
- **Design Lead Planning & Anti-Slop:** Apply `skills/frontend-design/SKILL.md` ([Anthropic Frontend Design](https://github.com/anthropics/skills/blob/main/skills/frontend-design/SKILL.md))—plan 4–6 specific hex colors, bold typography pairings, and layout concepts with deliberate character before coding; eliminate generic AI tropes.
- **Frontend Craft & Critique Dials:** Apply `skills/impeccable/SKILL.md` ([Impeccable](https://github.com/pbakaus/impeccable))—use design dials (`bolder`, `quieter`, `distill`, `typeset`, `polish`, `audit`), enforce token consistency (`DESIGN.md`), and run mechanical anti-pattern audits.
- **UI/UX Intelligence & Genre Systems:** Apply `skills/ui-ux-pro-max/SKILL.md` ([UI/UX Pro Max](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill))—match domain aesthetics to proven genres (Bento Grid, High-Density Dashboards, Minimalist Linear-Style, Modern SaaS, Dark Mode) with WCAG AA accessibility, Fitts's law target sizing (44×44px+), and zero cumulative layout shifts.
- **Modern Web Guidance (Google web.dev):** Apply `skills/modern-web-guidance/SKILL.md` for web-facing UIs (Core Web Vitals LCP/INP/CLS, semantic HTML, Baseline features, progressive enhancement).
- **Astryx Design System:** Available at `skills/astryx/SKILL.md`; not applied silently as a default—offer it to the owner when no design action has been taken.
- **Foundational Craft:** Adhere to `skills/web-design/SKILL.md` for responsive ergonomics, modular 8pt/4pt spacing scales, optical alignment, and complete state coverage (resting, hover, focus-visible, active, loading, empty, error).

**Design-system selection.** The owner's approved reference or existing product system takes precedence (SOI). If the owner has **not** supplied a `template-page/` or reference and has not taken any action on design yet, **ask the owner once** with concise A/B/C options (A: **Astryx** `skills/astryx/SKILL.md`, B: platform-native [Material Design 3](https://m3.material.io/) / [Apple Human Interface Guidelines](https://developer.apple.com/design/human-interface-guidelines/), C: custom/reference) rather than assuming a default silently. These options authorise an initial representative screen, not a silent redesign of an existing product. Record the chosen system and tokens in the project design notes; obtain the owner's decision before a major new visual commitment. A design system is not a package: reuse the existing stack and check current supported implementations before proposing any new dependency. Avoid mixing competing component styles; verify accessibility and visual quality in the actual implementation.

Every user-facing feature must look and behave like a coherent finished product. Follow the owner's reference and the existing design system; reuse established components. Without a reference, propose a concise direction suited to the audience and platform, show one representative screen, and obtain the owner's decision on a major new visual direction before spreading it across the product. Routine polish within the agreed direction needs no repeated approval.

**Motion defaults.** Include hover effects, smooth loading indicators, 3D motion, entrance reveals, micro-interactions and parallax in the visual design, adapted to the product and platform. Use subtle, purposeful effects and provide touch and keyboard equivalents for hover. Respect reduced-motion settings by removing or replacing spatial motion, including 3D, reveals and parallax, while keeping status and feedback clear. Avoid delaying access to content, blocking interaction or adding unnecessary dependencies; verify performance and the reduced-motion experience on representative screens.

- Establish consistent typography, spacing, alignment, colour, iconography and component states. Use clear information hierarchy, readable content widths and restrained decoration; avoid generic ornament that distracts from the task.
- Design the full experience per `skills/web-design/SKILL.md` (§7–8) where applicable: core data states (empty with CTA, loading skeletons/spinners, ideal, partial, overflow/max with truncation and pagination/infinite scroll), error & system pages (404, 500, 403, offline/cached retry, maintenance mode, session timeout with local draft save), form states (visible labels + helper text, focus/active, post-typing inline validation, disabled with tooltip, unsaved changes warning), feedback & micro-interactions (toasts/snackbars with Undo for destructive actions, confirmation modals, progress indicators, hover/pressed states), and first-time & accessibility states (onboarding/walkthroughs, search no results, keyboard Tab navigation + focus rings, image fallbacks). Use real approved content; do not ship placeholder copy, broken assets or dead controls.
- Adapt to the platform and relevant screen sizes, including long translated text. Check keyboard navigation, visible focus, labels, contrast, touch targets and reduced-motion preferences where relevant.
- Before delivery, inspect the rendered feature at representative sizes and exercise the key interactions. Correct clipping, overflow, inconsistent spacing and unclear actions; show the owner representative screenshots with any remaining limits. Source inspection alone is not visual proof. If rendering tools are unavailable, record visual review as blocked rather than claiming polish is verified.

## 4. Product rules learned the hard way

These apply to every project unless the owner says otherwise.

- **One feature, one map, one track, one test file, one doc.** A feature without all five is not finished.
- **Every language at once.** Add or change user-facing text in all supported languages in the same change. Tests check that every key exists and keeps its `{{placeholders}}`. Use the terms the app already uses in each language.
- **Gender-neutral wording** in every language. Consent and privacy first for sensitive features; gate them and never store private choices.
- **Versions and caches.** Bump the version the platform uses whenever something reaches users: web `?v=` pins and service-worker cache names, Android `versionCode`, iOS build number, package versions, API versions and migrations. `.loop/platform.md` says which. Stale caches and unchanged build numbers are the most common "it did not update" bugs.
- **No raw developer text for users.** No `alert()` with stack traces or "check console". Use a calm in-app message, translated; log technical detail quietly.
- **Measure before claiming.** Sizes, timings and savings only from real measurements. Sound, feel and device performance need a listening or device check; say when nobody has done it.
- **Plans are not features.** Ideas go to `FIX-QUEUE.md` or `planned` maps, never into delivered maps or release notes.
- **Legal checks travel with the feature.** A feature that touches personal data, cookies, third parties, licences, assets, payments, advice or claims is not delivered while its legal rows are `todo`. Loop drafts legal pages and flags `lawyer` items; it never claims the product is legally compliant.
- **Removal is a change.** Removing a feature updates its map, tests, locale keys and docs too.
- **Prefer HTTP query where possible.** For read, filter, search, inspection and other idempotent queries over HTTP, use HTTP query parameters (e.g. `GET /resource?filter=value`) rather than request bodies or ad-hoc custom headers. Keep mutations (`POST`, `PUT`, `PATCH`, `DELETE`) explicit and distinct from queries.

## 5. Evidence levels

Label every result with the highest level actually completed. A lower level never proves a higher one.

| Level | What it shows |
| --- | --- |
| `static` | Files, syntax, JSON, references, diffs |
| `unit` | A deterministic local test (with mocks where stated) |
| `runtime` | A real local process or HTTP response was exercised |
| `browser` / `emulator` / `staging` | Real interaction in the platform's own environment: a browser, an Android emulator or iOS simulator, a launched desktop app, or a deployed test server |
| `device` | Listening, feel, thermal or performance on a named real device or operating system |

The proof ladder for the chosen platform is in the project's `.loop/platform.md`. Browser, emulator or simulator tests and screenshots are used when the task is visual, structural or the owner asks; keep artifacts temporary and outside commits. Missing tools or services are `BLOCKED`, not app failures. Flaky tests are reported as flaky after a solo rerun, never hidden.

## 6. Safe development

- Inspect before editing. Preserve other people's work and intentional removals. Re-check files that another actor may have changed.
- Prefer focused, reversible changes. No destructive command without approval.
- Never expose or commit secrets, tokens, private data, browser state, `.DS_Store`, caches or temporary output. Inspect staged paths and `git diff --cached --check` before each commit.
- Register cleanup for every server, worker, timer and listener a test starts.
- No heavy infrastructure (Docker, microservices, new frameworks) without a measured reason and owner approval.
- Security follows [SECURITY.md](./SECURITY.md) at the level the project needs.

### Goal continuity and necessary rests

**Goal pauses belong to the owner.** Keep the goal active until it is complete. Never set it to paused unless the owner explicitly asks. Take necessary temporary rests (for example cooldowns, rate-limit waits or required recovery) without pausing the goal; record the reason and restart condition, then continue automatically when checks pass and the host permits. Continue other authorised work when safe. A rest never bypasses resource guards, approval gates or host limits. The owner may pause while riding or travelling and resume on arrival; do not infer a pause from absence or travel, and do not resume an owner-paused goal until the owner asks.

### Resource guards and pauses

When a project or host uses a resource guard (CPU, memory, disk, thermal, battery, quota or similar checks before work runs):

- **Rules by task profile.** Each rule says what it allows for `light` work and for `heavy` work. Explicitly approved light work may run when the readings it depends on pass, even if another reading is unknown. Unknown readings still block heavy work. A known warning blocks both.
- **Unknown is never safe.** Missing, empty, unreadable or stale telemetry is `unknown`. Never describe it as "cool", "clear", "safe" or "no problem".
- **A clear state needs a number.** A positive "no warning" state needs numeric evidence (for example macOS `pmset -g therm`: `Thermal Warning Level: 0` or `CPU_Speed_Limit = 100`). Text such as "no thermal warning level has been recorded" stays `unknown`. Parsers must test missing and numeric readings separately.
- **Test both profiles.** Guard tests cover light and heavy behaviour for each state: clear, warning and unknown.
- **Pause report.** On every necessary rest or owner-requested pause, tell the owner: the exact blocker; the latest reading and its time; what work is still allowed; the restart condition; and the ETA. Give a measured cooldown when there is one. When restart waits for a future outside reading, say "ETA unknown" — never guess a time.

## 7. Approval gates

Ask first before: deleting or overwriting material data; publishing or deploying; publishing legal text (privacy, terms, cookie, refund pages, disclaimers); releasing with any `lawyer` row in the legal checklist; sending messages or creating accounts; spending money; using credentials or systems outside the project; installing unapproved third-party packages outside the owner-approved project stack; major architecture or design-system commitments; choosing a public name.

Everything else that is local, reversible, part of the approved stack, or within the request goes ahead continuously without stopping.

## 8. Git and release

- Commit each validated checkpoint with a clear message and the session attribution the host requires. Local commits are fine without asking; pushes, merges to production and deploys follow the owner's authorisation.
- If the agent cannot push (no credentials), give the owner one copy-paste command and confirm the remote afterwards (`git fetch`, compare `HEAD`).
- Never reset, rebase or force over published or unrelated work. Use corrective commits.
- Clear stale lock files (`index.lock`, `HEAD.lock`) only when no git process is running, and only with delete permission.
- Keep Loop files, handoffs and the atlas out of production bundles, app packages and the public web root. Check the hosting configuration before claiming they are excluded.

## 9. Handoff and continuity

- `HANDOFF.md` starts with one `CURRENT RESUME` block: baseline commit, objective, decisions, owned files, fresh checks, limits, approvals, local vs published status, and the exact next action. Update it in place before every pause or reset.
- Older entries live below a history heading; they never override the current block. When history grows, move it unchanged to `handoff-archive/` with an index and append-only corrections.
- Durable truth lives in source, atlas, tracks, handoff and Git, not in chat memory.
- **One rule, one wording everywhere.** When a rule changes, update every place that states it in the same change: the stored goal or objective, `AGENTS.md`, `.loop/` files, tracks and the `CURRENT RESUME` block. Search for the old wording and remove it.
- **Report sync blockers separately.** If a copy cannot be edited (for example a stored goal whose text the available controls cannot change), record it as its own `BLOCKED` item: which copy, the old rule it still holds, and what the owner must do. Never say the goal or task has resumed while its stored text still carries the old rule. A docs fix does not update a stored goal.
- Progress is measured from the atlas (the atlas status command in `AGENTS.md`: maps delivered / total) plus the owner-approved scope. Do not invent completion percentages.

## 10. Completion

A release is complete when every map in its scope is `delivered`, required checks pass on the integrated source, the legal checklist final audit (check 20) is done with no `todo` or `blocked` rows and an owner decision on every `lawyer` row, docs and handoff are current, cleanup passed, and nothing blocks within scope. The final report gives: what shipped, how to run it locally, the checks and their evidence levels, what is not verified, and the release command or the confirmed remote state. Production readiness, security clearance and legal status are reported separately. Legal status is the checklist count (done / n/a / blocked / lawyer), never a claim of compliance.

## 11. Policy maintenance

Change this policy only in explicit framework work requested by the owner. Keep policy commits separate from application commits. A project may keep a local copy under `Loop/` that is newer than the installed plugin; editing the project copy does not update the plugin cache. The previous full policy is preserved in `archive/v0.3.1/loop.md`.
