# Idea 0021: shrink the always-loaded agent instruction weight

- Date: 2026-07-11
- Status: seed
- Parent: [0020](0020-use-the-method-economically-and-token-saving.md)

## Why this budded from 0020

Idea 0020 asked how to *operate* the method economically; it was **decomposed**
(ADR-0027) into three axes. This idea is one of them. The full split:

- **Resume discipline (sibling [0023](0023-name-the-resume-time-economy-practices-as-a-discipline.md)).**
  The cost an agent pays *only when it reads the trail* — and can already avoid:
  resume via `overview.md`, grep headers not bodies, targeted reads. Opt-in waste;
  purely advisory to fix.
- **Always-loaded weight (this idea).** The cost an agent pays *every session,
  unconditionally* — `AGENTS.md` is injected as custom instructions before any task
  begins. This is the larger, unavoidable spender, and reducing it is a concrete
  refactor. That is the distinct thought worth its own thread.

A closely related but separable thought — moving the method's fixed *procedures*
into invokable skills — is the third sibling, idea 0022. This idea is about
compacting the prose that stays; skills would enable *deeper* compaction later.

## Observation

One structural fact makes the always-loaded file heavy: **`AGENTS.md` states its
rules ~3×.** The same normative content (ordinal numbering, per-family status,
canonical header format, disentangling procedure) appears in `## The lifecycle`,
again inline in prose, and again in full in `## Agent operating guidance`. Every
session pays for all copies. A rough audit suggests ~30–40% could go with zero
loss of meaning by stating each rule once and cross-referencing.

## Desired means (sketch)

- **State each rule once.** Collapse the triple-statement into a single normative
  block; let other sections cross-reference rather than restate.
- **Keep `AGENTS.md` to principles + pointers.** Long how-to step lists (overview
  refresh, insert-and-shift, disentangling, adopter update) become pointers rather
  than inline procedures — dovetailing with the skills idea (0022).
- Estimated ~21 KB → ~13 KB, saving ~2k tokens on **every** session.

## Open questions / tensions

- **Compaction vs. the derived-rendering sync (ADR-0014).** `AGENTS.md`'s method
  body is regenerated from `working-method.md`. Compaction must happen at the
  *canonical* source (or in the rendering rules), not as a hand-patch — otherwise
  the next regeneration undoes it. Which layer gets compacted: the canonical spec,
  the derivation rules, or the non-derived `## Agent operating guidance` section?
- **Human readability vs. terseness.** The repetition may aid a human reader
  skimming one section. Does stating-once hurt the human audience the split
  renderings (ADR-0014) were meant to serve?
- **Is this even a mechanism change, or just a refactor?** If purely a
  tightening of existing prose with no behavioral change, it may need no ADR — or a
  light one. Decide when promoting.
