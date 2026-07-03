# Travel diary

An informal, growing logbook of the journey — an optional, **human-facing**
companion to `docs/overview.md`. Where the overview is a derived, terse status
index, this file is loose prose: a friendly trail of *"where were we, and where
were we headed"* that a colleague can skim after a break.

The artifacts under `docs/ideas/`, `docs/decisions/`, and `docs/plans/` remain the
**source of truth**. This file touches none of them and is never authoritative; it
can be as loose as it likes.

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

<!-- Entries go here, newest first. Delete this comment when you add the first one. -->
