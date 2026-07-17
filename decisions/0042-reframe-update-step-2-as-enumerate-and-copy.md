# ADR-0042: Reframe update step 2 as an enumerate-and-copy operation

- Date: 2026-07-17
- Status: accepted
- Promoted from: [idea 0036](../ideas/0036-step-2-copy-everything-still-relies-on-agent-judgment.md)
- Amends: [ADR-0022](0022-every-release-ships-reliable-update-instructions.md)

## Context

v2.18.1 (ADR-0041) fixed the *immediate* v2.18 miss by reframing `updating.agent.md`
step 2's example list as *explicitly non-exhaustive* — "copy **everything** under
`starter/`, including but not limited to …". That made under-copying **wrong**, but
not **impossible**: step 2 is still a prose paragraph the agent reads and interprets
to decide *which files* to copy. The original miss happened because an agent narrowed
a copy that prose told it to widen; non-exhaustive wording discourages that narrowing
without removing the room for it. Under the next new subtree, the same class of miss
can recur.

The operation step 2 actually wants is mechanically trivial: **mirror the `starter/`
tree** into the adopter's `docs/`, then **subtract** a small, already-enumerated
*preserve* set (project-authored artifact families, populated companions,
`overview.md`). The fragile open-ended side ("did I get every file?") is a whole-tree
copy; the only judgment left is the short closed "what do I protect?" list.

## Decision Drivers

- Remove the room for interpretation at the **source**, not with safety nets bolted
  on after (ADR-0041 already weighed and dropped tree-parity + a conformance item as
  over-engineering; that judgment holds).
- Keep the copy-driven contract intact (ADR-0022): `starter/`'s contents stay the
  single source of truth; no manifest.
- Keep it cheap — a wording refinement, no new mechanism, no new human step
  (ADR-0031).

## Considered Options

1. **Leave step 2 as-is.** v2.18.1's non-exhaustive wording may be judged good
   enough. Cheapest (zero work), but preserves the interpret-a-paragraph fragility
   that already failed once.
2. **Add safety nets** (post-copy tree-parity check, conformance item). Catches a
   miss after it happens, for any scaffold — but ADR-0041 already rejected this as
   over-engineering for a wording bug, and it adds per-update ceremony.
3. **Iterate-and-copy every detected subfolder, minus a preserve-list (chosen).**
   Recast step 2 so the agent **enumerates the subfolders it detects** under the
   source's `starter/docs/` and copies each one wholesale (overwriting), *except* the
   short, fixed set of project-authored folders/files it must never overwrite. A new
   subfolder is picked up because it is *discovered*, not because it was *named* —
   turning "which files ship" from a judgment call into a mechanical enumerate-copy.

## Decision

Adopt option 3. Reframe `updating.agent.md` step 2 so its **primary instruction is
to enumerate and copy every detected subfolder** — not to work from an example list.
State it as one deterministic rule:

> **Copy every subfolder detected under the source's `starter/docs/`, with all its
> contents, overwriting existing versions — *except* the project-authored
> folders/files, which are never overwritten:** `docs/decisions/`, `docs/ideas/`,
> `docs/plans/`, a populated `docs/travel-diary.md`, `docs/intermediate-artifacts/`,
> and `docs/overview.md` (regenerated in step 5, not copied). Copy the method text
> and templates at the `docs/` root the same way.

Because the agent *discovers* the subfolders rather than reading a named set, a new
scaffold subtree (like v2.18's `docs/scripts/`) is picked up automatically — the very
miss that started this thread cannot recur, and no future subfolder needs its own
instruction line. The only reasoning left is the short, stable **preserve-list** of
what *not* to overwrite. `starter/` remains the single source of truth; no manifest
is introduced. This **amends ADR-0022** in execution detail only — the copy-driven
mechanics are unchanged; it sharpens *how* the copy is expressed so it cannot be
under-scoped.

Ship it as a **patch release (2.18.2)** — a pure wording refinement with no
adopter-visible behavioral change. Its `CHANGELOG` migration note is **"none"**: an
adopter already on v2.18.1 (or a fresh v2.18.2 adopter) gains nothing to *do* — the
enumerate-and-copy lands exactly the same files; this only makes a *future* under-copy
harder to author. (The already-stranded v2.18 adopter was remediated by v2.18.1's
non-"none" note; that channel is not reopened here.)

## Consequences

- **The fragility is removed at the source** — step 2's copy scope is *every
  detected subfolder* by construction, so no example list can be read as closed and
  no future subfolder can be dropped by narrowing a paragraph.
- **ADR-0022 untouched in substance** — an execution-detail amendment; on acceptance
  add the reciprocal `Amended by: ADR-0042` to ADR-0022 (alongside the existing
  `Amended by: ADR-0041`).
- **No new ceremony** — no tree-parity check, no conformance item; consistent with
  ADR-0041's over-engineering call. The preserve set is unchanged.
- **Audience split preserved (ADR-0031)** — agent-facing procedure only; the human
  trigger and `adopting.md` are untouched.
- **Follow-on:** on acceptance, a `draft` stub plan `Implements:` this ADR to reframe
  step 2 as enumerate-detected-subfolders-minus-preserve-list, add the `CHANGELOG`
  **2.18.2** entry with the
  "none" migration note, bump the three `starter/` citations v2.18.1 → **v2.18.2**,
  and add the reciprocal `Amended by: ADR-0042` to ADR-0022.
