---
name: loop
description: "Use when the user says 'Use Loop for this project', 'Apply Loop', 'Resume with Loop', 'Build the next atlas map', or asks for Loop project orchestration. Asks which platform to build for at the start, then starts new projects atlas-first with loop-init.mjs, adopts existing projects, builds one atlas map at a time with proof, and keeps a single CURRENT RESUME handoff."
---

# Loop orchestration (atlas-first)

Apply `loop.md` from the project-local `Loop/` folder when present, otherwise from the plugin root. Companion files: `ATLAS-FIRST.md` (atlas format and build loop), `OWNER-COMMUNICATION.md`, `EFFICIENT-WORKFLOW.md`, `DELIVERY-WORKFLOW.md`, `SECURITY.md`, `LEGAL-CHECKLIST.md` (20 legal checks), `MODEL-ROUTING.md`. The project copy may be newer than the installed plugin; do not edit the installed cache.

## Invocation

An explicit request to use or resume **Loop** selects this skill immediately. Loop is this local workflow, not an OpenAI product term: do not open OpenAI Docs or search the web to identify it. Never ask the user to pick a task class; infer it.

If the prompt contains `[LOOP_ROUTED_CHILD]`, this is already a routed bounded task: do not classify or dispatch again. Do only that task, validate it, and return.

## New project (empty folder or new idea)

Loop asks the questions and then starts building. Do not wait for a separate approval once the answers are enough.

1. Read-only check of the target. A filled `START.md` there means: read it, ask only what is missing. A `template-page/` folder there is the owner's basic template page.
2. Otherwise ask the questions from `start/START.md` (Loop root) in **one** message, numbered, plain words: name; for whom; what the first release must do; **which platform** (web, Android, iPhone, both mobile, desktop, backend/API, command-line, other, or several); stack or "to decide" (and whether standard stack package installs are pre-approved); languages and target user countries/regions; features/pages with steps; must-not-do; and design direction (template page/reference, or A: Astryx, B: platform-native Material 3 / Apple HIG, C: custom). If unsure about platform or stack, give A/B/C options with a recommendation; never choose for them. No files, Git or installs before the answers.
3. Write the answers into `<target>/START.md` and any template files into `<target>/template-page/`.
4. When name, platform and at least one feature are known, run from the Loop root:

   ```
   node scripts/loop-init.mjs <target-folder> --git
   ```

   It reads `START.md` (moved to `docs/START.md`), moves the template page to `design/template-page/`, and creates `AGENTS.md`, `HANDOFF.md` (one CURRENT RESUME block), `.loop/workflow.md`, `.loop/platform.md` (stack, test commands, proof ladder, platform rules, release path), one track per map and `docs/app-map/` (atlas data, builder, status, atlas check, `index.html`). Feature maps and the `release` map start `planned`. JavaScript projects also get `npm run atlas*` scripts; others use the plain `node docs/app-map/...` commands listed in `AGENTS.md`.
5. Build straight away: one line on the atlas overview, then the build loop below on the first map. Every screen follows `design/template-page/` when it exists. Report each delivered map with proof and carry on to the next. Stop only at approval gates or real product decisions.

## Existing project

Read `AGENTS.md`, `HANDOFF.md` (CURRENT RESUME only), `.loop/platform.md`, then the atlas status command from `AGENTS.md`. If the project has no atlas yet, run `node scripts/loop-init.mjs <project> --adopt --name "<Name>" [--platform <id>]` (it never overwrites files and reports the detected platform), then map current behaviour as `delivered` maps with real `file:line` sources before planning new work. Preserve unrelated changes; reconcile docs with code.

## Build loop (one map at a time)

Follow the canonical execution order and Sūtra 1.4.2 rule resolution from `loop.md` §3 (**SOI**: more specific rule wins on the same operand; **DOI**: right-side suffix/gate resolves on its own operand before merging into the left base):

1. **Read Hot memory & lock the left base:** Read `HANDOFF.md` (`CURRENT RESUME`), `.loop/platform.md`, and run the atlas next command → select the single ready active map (or first dependency-ready map in `meta.buildOrder`) and its track. Resolve invalid plans or checkpoint blocked active work before choosing another map. Never trigger domain skills before knowing the active map and its operands.
2. **Resolve SOI & attach right-side triggers by operand:** Confirm the map's steps (`planned` → `building`), then attach only matching triggers:
   - **UI / Visual operand:** Trigger `skills/design-inspiration/`, `skills/modern-web-guidance/` (for web), `skills/frontend-design/`, `skills/impeccable/`, `skills/ui-ux-pro-max/`, `skills/web-design/`, and `skills/astryx/` (when chosen by the owner), and audit with `skills/ai-slop-detector/` before delivery.
   - **Data / Auth / API / Payment / Asset operand:** Update matching rows in `.loop/legal-checklist.md` (trigger table in `LEGAL-CHECKLIST.md`).
   - **High-risk / Bounded offload operand:** Apply `MODEL-ROUTING.md` and `EFFICIENT-WORKFLOW.md` (stay `direct` unless a bounded child or specialist review adds clear value).
3. **TDD (RED → GREEN → REFACTOR):** Confirm RED, implement GREEN, then refactor. Reuse coverage; unit-test changed logic and integration-test changed boundaries, including applicable failure paths (`DELIVERY-WORKFLOW.md`). Record mocks, blocked checks and not-applicable levels.
4. **Apply design, motion & transport gates (when applicable):** Think like a front-end designer (`loop.md`), preserve the owner's `template-page/` or existing design system (SOI). If the owner has not taken any action on design yet, ask once with A/B/C options (A: **Astryx** `skills/astryx/SKILL.md`, B: platform-native Material Design 3 / Apple HIG, C: custom/reference) instead of defaulting silently. Apply `skills/modern-web-guidance/SKILL.md` for web UIs, cover all applicable states from `skills/web-design/SKILL.md` §7–8, motion defaults with reduced-motion alternatives, HTTP query parameters for idempotent reads, and verify rendered screens at representative sizes. Prove at the strongest level in `.loop/platform.md` and state the level reached. No touched legal row may stay `todo`.
5. **Two-stage review & security gate:** Run `SPEC_COMPLIANCE` before `QUALITY_AND_RISK` (`DELIVERY-WORKFLOW.md`), then perform the feature security review in `SECURITY.md`: auto-fix routine/low/medium findings directly, rerun tests and re-review; stop to discuss with the owner only for critical/high architectural or breaking security trade-offs. While awaiting discussion keep the goal active, checkpoint and return the map to `planned` with `blockedBy` before selecting other ready work.
6. **Merge & close the base (Tripādī one-way finalization, `8.2.1`):** Verify seam compatibility (*Samartha*/*Sandhi*), flip the map to `delivered` with real `file:line` sources (the atlas build refuses fake or missing sources), run product tests and atlas check, update the single `CURRENT RESUME` block in `HANDOFF.md`, and commit with a checkpoint id. Minor polish goes to `FIX-QUEUE.md` rather than reopening earlier design/discovery loops; only critical/high blockers reopen the base.
7. **Continuous page & major-feature flow (no micro-stops):** Do not stop on simple steps, routine boilerplate, approved stack installs, or small sub-tasks. Keep building continuously across related sub-steps until a cohesive **page or major feature** is complete and proved, then report to the owner in plain words with a screenshot when visual, and repeat.

On the first map, mark every legal check `todo` or `n/a` (with reason) from the brief (using the countries/regions captured at kickoff; ask only if missing). Before release, run check 20 (final legal audit): no `todo` or `blocked` rows, and an owner A/B/C decision on every `lawyer` row. Loop drafts legal pages; it never claims legal compliance.

**Goal pauses belong to the owner.** Keep the goal active until it is complete. Never set it to paused unless the owner explicitly asks. Take necessary temporary rests (for example cooldowns, rate-limit waits or required recovery) without pausing the goal; record the reason and restart condition, then continue automatically when checks pass and the host permits. Continue other authorised work when safe. A rest never bypasses resource guards, approval gates or host limits. The owner may pause while riding or travelling and resume on arrival; do not infer a pause from absence or travel, and do not resume an owner-paused goal until the owner asks.

Resource guards (CPU, memory, disk, thermal): rules by task profile — approved light work may run when its checks pass; unknown readings block heavy work; a known warning blocks both. Unknown is never "safe", and a clear state needs a numeric reading. Every necessary rest or owner-requested pause reports blocker, latest reading and time, what is still allowed, restart condition and ETA (measured, or "unknown"). When a rule changes, update every copy (goal, `AGENTS.md`, `.loop/`, tracks, handoff); a copy that cannot be edited is its own `BLOCKED` item, and the goal is not reported as resumed.

Release, push, spending, data deletion, publishing legal text and user-visible content changes stay behind the approval gates in `loop.md`. When the owner must push, give one copy-paste command and confirm with `git fetch` afterwards.

## Prioritise before starting work

Keep one active delivery map (the current big rock). Finish its supporting fixes, tests and docs before unrelated work. Dependencies come first; then the smallest valuable outcome and risk reduction. `meta.buildOrder` is the agreed order; the Eisenhower matrix is triage, not an automatic override. Record blockers and reasons for reordering. Before switching from a blocked active map, checkpoint its restart step in the track and handoff and return it to `planned` with `blockedBy` retained. Multiple building maps are invalid; priority never bypasses dependencies or release boundaries. See `ATLAS-FIRST.md` → Priorities and one active big rock.

## Routing & memory

- **Memory tiers:** Keep working context in **Hot** memory (`HANDOFF.md` `CURRENT RESUME`, active map, targeted source ranges); store durable per-feature details in **Warm** memory (`.loop/tracks/<id>/`, `FIX-QUEUE.md`); keep **Cold** memory (`handoff-archive/`, `archive/`) unread unless investigating history.
- **Agent calling & routing:** Stay `direct` when the current agent meets capability and context bounds. Dispatch a bounded child (`[LOOP_ROUTED_CHILD]`) only for distinct ownership, capability/context mismatch, or independent specialist review—following the calling order **Coordinator → Bounded Worker → Reviewers (`SPEC_COMPLIANCE` then `QUALITY_AND_RISK`) → Coordinator Integration**. Use the host's native subagent/model-routing mechanism when available (or `scripts/codex_model_router.py` as an optional adapter under Codex CLI; it reads only `[LOOP_CLASSIFY]` … `[/LOOP_CLASSIFY]`, applies per-run overrides, and never rewrites global config). If automatic switching is unavailable, recommend a model, keep a resumable checkpoint, and ask the engineer to switch with the host selector (for example `/model`). Never claim a switch you did not see.

## Boundaries

Browser, emulator or simulator checks and screenshots are used when the change is visual or the owner asks, through the project's tests or the atlas verify command. Destructive or history-changing recovery needs approval. The skill orchestrates; the project's source, tests, atlas and handoff are the record.
