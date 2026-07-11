# ADR-0007: Seal the method: AGENTS.md is the single source of truth

- Status: accepted
- Date: 2026-06-28
- Amends: ADR-0006 (reverses where the contract lives)
- Amended by: ADR-0014 (re-frames the single source of truth as the lean spec in `working-method.md`; this repo's `AGENTS.md` becomes a derived rendering)

## Context

ADR-0006 made `AGENTS.md` the tool-agnostic entry point but deliberately
*deferred* migrating the eight-promise contract into it: the contract stayed in
`.github/copilot-instructions.md`, and `AGENTS.md` merely linked to it. ADR-0006
named that migration as a future decision.

The method is now structurally complete (ADR-0001 to ADR-0006): every lifecycle
stage is mechanized, the layout and cross-links are fixed, and there is an entry
point. The concept phase is finished. Two things remain to give the repo a
*settled and sealed* character:

- the contract and its surrounding context still live in a Copilot-specific file
  whose header even claimed the mechanics were "not yet decided" — now false;
- there is no single canonical document a reader can trust as complete.

The promises in play:

- **Economy** (#2): one source of truth, not a contract split across files that
  can drift.
- **Genericity** (#7): the canonical description must be tool-agnostic, not bound
  to one assistant's instruction file.
- **Borrow, don't invent** (#8): `AGENTS.md` is the cross-tool hand-off standard;
  it is the right home.

## Decision

`AGENTS.md` becomes the single, canonical, tool-agnostic source of truth for
`the-way`, and the repository is sealed.

- The eight-promise contract, the origin story, and the agent operating guidance
  (confirmation guard, custom-agents note) are migrated **into** `AGENTS.md`.
  This reverses ADR-0006's choice to keep the contract in
  `.github/copilot-instructions.md`.
- `.github/copilot-instructions.md` is reduced to a thin pointer to `AGENTS.md`,
  so the two cannot diverge (Economy #2). Any future tool file (e.g. a
  `CLAUDE.md`) does the same.
- `README.md` is rewritten from "concept phase / not yet decided" to a settled
  summary that points at `AGENTS.md`.
- `AGENTS.md` and `README.md` carry a **"settled & sealed"** status: the concept
  phase is complete. The method now exists to be *used*. Any later change to
  `the-way` itself is made the-way — proposed and recorded as a new ADR, with
  amended or superseded ADRs cross-linked, never edited away (Agility #5).

## Consequences

- There is now one canonical document. A reader or agent trusts `AGENTS.md` as
  complete; tool files and the README only point to it (Continuity #1,
  Economy #2).
- The canonical description is tool-agnostic, completing the intent ADR-0006
  deferred (Genericity #7, Borrow #8).
- The repository's character changes from *under construction* to *settled*. The
  ADR log (`decisions/0001`–`0007`) stands as the complete record of how the
  method was built. Sealing is not locking: the method explicitly provides for
  its own future amendment through new ADRs.
- This is the capstone decision of the concept phase; with it, `the-way` is done.
