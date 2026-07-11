# Idea 0022: render the method's fixed procedures as optional skills

- Date: 2026-07-11
- Status: seed
- Parent: [0020](0020-use-the-method-economically-and-token-saving.md)

## Why this budded from 0020

Idea 0020 asked how to *operate* the method economically; it was **decomposed**
(ADR-0027) into three axes. One driver of the cost an agent pays every session is
that the method's fixed **procedures** are carried as step-by-step prose in the
always-loaded `AGENTS.md`. Sibling idea 0021 handles the *compaction* of that file
and sibling idea 0023 the *resume-time* discipline; this idea is the distinct,
mechanism-adding thought: move the procedures themselves into **invokable skills**
loaded only when needed. The three share 0020's motivation but are separable —
compaction is a refactor of existing prose, skills add a new (optional,
tool-specific) mechanism — so they get their own threads.

## Observation

Several method operations are **lookups, not judgment calls** — deterministic step
lists that only matter *when invoked*, yet today they sit in always-loaded context
taxing every session that never runs them:

- regenerate `overview.md` (header scan → rewrite the three tables);
- create the next artifact (max+1 slot, verify unused, canonical header);
- insert-and-shift renumber;
- disentangle a large idea (the fixed budding procedure);
- adopter update / conformance check (already do-guidance in `adopting.md`).

## Desired means (sketch)

Package these as optional **skills / commands** loaded **only when triggered**.
Two benefits:

- **Smaller always-loaded context** — the step lists leave `AGENTS.md`, which
  keeps only *principles + when to invoke which procedure*.
- **More reliable execution** — an executable skill is followed more faithfully
  than a step list buried in prose (cf. the ADR-0026 "bare header silently missed"
  failure class, where a procedural detail was easy to overlook).

## Open questions / tensions

- **Tool-agnosticism (ADR-0006) vs. skills.** Skills are somewhat tool-specific,
  and the method prizes plain-markdown transparency (promise #3). Clean framing:
  the procedures stay **canonical prose in the method**; skills are an *optional,
  derived, tool-specific rendering* of them — the same relationship `AGENTS.md`
  already has to `working-method.md` (ADR-0014). Does that framing hold?
- **Source of truth / sync (ADR-0014).** If skills are derived, they must
  regenerate from the canonical procedure text, never drift into a second
  authority. What keeps them in sync?
- **Do skills ship in `starter/` so adopters inherit them, or are they home-repo
  tooling?** If canonical prose is the source of truth, adopters could regenerate
  their own skills for their own toolchain; the method need not ship any.
- **Relationship to compaction (0021).** Skills *enable* deeper compaction (once a
  procedure lives in a skill, its prose can shrink to a pointer), so the two ideas
  likely inform each other at promotion even though each gets its own ADR.
