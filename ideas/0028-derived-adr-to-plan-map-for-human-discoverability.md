# Idea 0028: a derived ADR→plan map so a human can find how a decision was implemented

- Date: 2026-07-11
- Status: promoted
- Promoted to: [ADR-0034](../decisions/0034-derived-adr-to-plans-sub-index-in-overview.md)

## Observation

A human reading an accepted ADR and wondering *"how was this implemented?"* has no
one-click path to the plan(s) that carry it out. The `Implements:` cross-link is
**forward-only** (plan → ADR), deliberately: one ADR can accumulate several plans,
and ADR-0012 declined a reciprocal ADR→plan back-link because a write-once
reciprocal breaks the moment the reverse side is not 1:1 — and because editing a
settled ADR every time a new plan appears invites churn and drift.

That reasoning is sound and should stand. But it leaves a real, narrow
**human-discoverability** friction on the ADR side:

- an **agent** resolves it instantly — grep `Implements:.*NNNN` across `plans/`, or
  just ask;
- a **human** reading the rendered markdown has nothing to click — they must grep,
  scan, or ask the agent.

## The candidate

Close the gap the *method-consistent* way — **derived, not hand-maintained** — by
surfacing the already-existing `Implements:` relationship in `overview.md`:

- Add an **`Implements`** column (or a small derived "which plans implement each
  ADR" view) to `overview.md`, generated from the plans' `Implements:` headers
  during the normal wholesale regeneration.
- This gives a human an **always-current ADR↔plan map** with **zero hand-upkeep**,
  **no reciprocal field on the settled ADR**, and full consistency with ADR-0012
  (no ADR→plan back-link) and ADR-0011 (`overview.md` is a derived, regenerated
  snapshot).

## Why this deserves a thread

It is **generic** — every adopter's humans hit the same "how was this ADR
implemented?" question — so any change belongs in the method (spec + the
`overview.md` refresh procedure), not just this repo.

It is also carefully **not** a reopening of ADR-0012: the fix adds a *derived view*,
never a maintained forward link on the ADR. If accepted, it likely **amends**
ADR-0011's overview-shape definition rather than touching ADR-0012 at all.

## Open questions — resolved

- **Shape of the derived view.** Resolved: a dedicated ADR-oriented sub-index
  (ADR → its plans), not a column on the existing plan table — it answers the
  question in the reading direction the use case actually needs.
- **What to render.** Resolved: for each ADR, list the implementing plan(s) with
  their status (`draft` / `active` / `done` / `abandoned`), so a human sees
  implementation progress at a glance without opening the plan.
- **Cost vs. payoff.** Resolved: worth it — the sub-index is zero hand-upkeep
  (derived during the normal wholesale regeneration) and closes a real
  discoverability friction; not YAGNI.
- **Which ADR does it amend?** Resolved: amends ADR-0011 (overview shape/refresh
  procedure) only. ADR-0012 (no ADR→plan back-link) stays untouched — this is a
  derived view, not a reciprocal field.
