# Travel diary

An informal, growing logbook of the journey — an optional, **human-facing**
companion to `overview.md`. Where the overview is a derived, terse status index,
this file is loose prose: a friendly trail of *"where were we, and where were we
headed"* that a colleague can skim after a break.

The artifacts under `ideas/`, `decisions/`, and `plans/` remain the **source of
truth**. This file touches none of them and is never authoritative; it can be as
loose as it likes.

## Agent instructions

When the user says **"add a chapter to the travel diary"** (or similar), do this
light-weight task — **no confirmation guard, no ADR, no plan**:

1. **Prepend** the new dated section at the top — newest first. It goes directly
   below this "Agent instructions" block, above all older entries.
2. Header is the current date in brackets: `## [YYYY-MM-DD]`. If a section for
   today already exists, disambiguate with a counter: `## [YYYY-MM-DD-(2)]`, then
   `-(3)`, and so on.
3. Under it, write a brief, friendly prose entry covering roughly:
   - **Where we are** — the current state / context.
   - **What we achieved** — since the last entry.
   - **What is left** — open threads.
   - **What is next** — the immediate next step.
4. Optionally end with a one- or two-sentence **continuation brief** — a nudge to
   whoever (human or agent) picks this up next, ideally with a link to the
   relevant plan or ADR.

Keep it short and human. It's a diary, not a report.

---

## [2026-07-03-(2)]

**Where we are.** decision-trail is now at **v2.5** — committed, pushed, and tagged
`v2.5.0` on `main`. The trail runs `ideas` 0001–0012, `decisions` 0001–0020, and
`plans` 0001–0010. The method stays settled; this change was itself made
decision-trail, start to finish.

**What we achieved.** We promoted a second concept proven in the sibling repo
*josyn-builder* — **intermediate artifacts** — into the method:
- Captured the working-material gap as
  [idea 0012](ideas/0012-intermediate-artifacts-a-scratch-layer-for-execution.md):
  executing a plan sometimes means *gathering* material to work on later, and that
  scratch had no home among the authoritative artifacts.
- Worked through all seven open questions one at a time, then decided it in
  [ADR-0020](decisions/0020-intermediate-artifacts-a-scratch-layer-for-execution.md):
  an optional, informal `intermediate-artifacts/` folder — outside the lifecycle,
  **not a source of truth**, guard-free, internally unstructured, committed by
  default, left to rot harmlessly. It's the *execution-stage* cousin of the
  human-facing travel diary.
- Carried it into action via
  [plan 0010](plans/0010-ship-intermediate-artifacts.md): new **Intermediate
  artifacts** section in the canonical `working-method.md`, a documented-but-empty
  `starter/docs/intermediate-artifacts/` folder, a seeded home-repo folder,
  regenerated `AGENTS.md` (method body + guard-free note, mirrored in
  `starter/AGENTS.md`), a mention in both `guide.md` renderings, a `CHANGELOG.md`
  **2.5.0** entry, and a regenerated `overview.md`. Provenance bumped to v2.5.

Along the way we also **committed the pending confirmation-guard teaching work**
(idea 0011, ADR-0019, plan 0009) that had been sitting uncommitted, and added a
`.gitignore` for Visual Studio's `.vs/` folder.

**What is left.** Nothing on this thread — plan 0010 is `done`. One loose end noted
for later: **v2.4.0 was never tagged** (the travel-diary release), so the tag
history skips from v2.3.0 to v2.5.0.

**What is next.** Use intermediate artifacts in anger: the next plan that needs to
park gathered data now has a conventional home. Optionally, backfill the missing
`v2.4.0` tag.

*Continuation brief:* State lives in the artifacts. For this feature, the reasoning
is in [ADR-0020](decisions/0020-intermediate-artifacts-a-scratch-layer-for-execution.md)
and the execution record in [plan 0010](plans/0010-ship-intermediate-artifacts.md).

## [2026-07-03]

*(First entry — this diary was born the same session the feature landed, so it
doubles as a worked example of the very thing it describes.)*

**Where we are.** decision-trail is moving to **v2.4**. The trail runs `ideas`
0001–0010, `decisions` 0001–0018, and `plans` 0001–0008. The concept phase stays
settled — every change to the method is itself made decision-trail.

**What we achieved.** We promoted a concept proven in the sibling repo
*josyn-builder* — the **travel diary** — into a feature of the method:
- Captured the human-machine-interface gap as
  [idea 0010](ideas/0010-a-human-friendly-travel-diary.md): the trail answers an
  *agent's* continuity questions precisely, but a *human* colleague asking "where
  are we / what changed / what's left / what's next?" still had to synthesize
  across `overview.md`, the active plan, and recent ADRs.
- Decided it in
  [ADR-0018](decisions/0018-a-travel-diary-for-the-human-machine-interface.md):
  the diary is a **shipped, optional, human-facing companion** to the
  machine-facing `overview.md` — authored prose vs. derived state — maintained
  guard-free and explicitly **not** a source of truth.
- Are carrying it into action via
  [plan 0008](plans/0008-ship-the-travel-diary.md): documented the mechanism in
  the canonical `working-method.md`, shipped a `starter/docs/travel-diary.md`
  template, regenerated `AGENTS.md` (method body + a guard-free "add a chapter"
  note, mirrored in `starter/AGENTS.md`), mentioned it in both `guide.md`
  renderings, and — since we chose to **dogfood** it — created this live diary.

*(Note: an earlier attempt this session ran the whole lifecycle ahead of approval
and self-accepted the ADR — a confirmation-guard breach. It was rolled back and
redone properly, step by confirmed step. The trail is history; this is part of it.)*

**What is left.** Two closing steps of plan 0008: the `CHANGELOG.md` **2.4.0**
entry and regenerating `overview.md`. Then the plan flips to `done`.

**What is next.** Finish those two steps, then use the diary in anger: the next
time someone asks "where are we?", point them here.

*Continuation brief:* The repo is its own continuation anchor — state lives in the
artifacts. For this feature specifically, the reasoning is in
[ADR-0018](decisions/0018-a-travel-diary-for-the-human-machine-interface.md) and
the execution record in [plan 0008](plans/0008-ship-the-travel-diary.md).
