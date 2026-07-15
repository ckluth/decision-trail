# ADR-0034: A derived ADR → plans sub-index in `overview.md`

- Status: accepted
- Date: 2026-07-11
- Promoted from: [idea 0028](../ideas/0028-derived-adr-to-plan-map-for-human-discoverability.md)
- Amends: ADR-0011 (extends the overview's shape with a second, ADR-oriented view)
- Amended by: [ADR-0038](0038-stub-plan-at-acceptance-and-derived-no-plan-backstop.md)

## Context

The `Implements:` cross-link (ADR-0005, ADR-0012) is deliberately forward-only:
a plan points to the ADR it carries out, and one ADR can accumulate several
plans over time. ADR-0012 declined a reciprocal ADR→plan back-link because a
write-once reciprocal field breaks the moment the reverse side is not 1:1, and
because editing a settled ADR every time a new plan appears invites churn and
drift.

That reasoning holds. But it leaves a narrow, real friction on the *human* side:
an agent resolves "how was this ADR implemented?" instantly by grepping
`Implements:.*NNNN` across `plans/`; a human reading the rendered markdown has
nothing to click and must grep, scan, or ask the agent. `overview.md`
(ADR-0011) already lists plans with their `Implements:` target implicitly
available from the plan header, but today's Plans table is not organized to
answer the question in the ADR's reading direction.

### Decision drivers

- **Transparency (#3):** a human should be able to answer "how was this
  decided thing implemented?" by reading a plain markdown file, not by asking
  the agent or grepping.
- **Economy (#2):** the answer must be free — derived from data the plans
  already carry (`Implements:`), with no new hand-maintained field anywhere.
- **Agility (#5) / avoid reopening ADR-0012:** the fix must not add a
  reciprocal field to the ADR itself, since that is exactly the write-once
  churn ADR-0012 ruled out. The view lives only in the *derived* `overview.md`.

## Decision

Extend `overview.md` (ADR-0011) with a second, derived view alongside the
existing three family tables: an **ADR → plans sub-index**, generated during
the same wholesale regeneration and from the same source data (each plan's
`Implements:` header field) — no new hand-maintained field, no back-link on
the ADR itself.

- **Shape.** A dedicated sub-index keyed by ADR (not a column bolted onto the
  existing Plans table), because it must answer the question in the direction
  a human actually asks it: "this ADR — which plan(s) implemented it, and
  where do they stand?" A column on the Plans table would still require
  scanning every plan row to answer that question; a dedicated index answers
  it directly.
- **Content.** For each ADR that has at least one implementing plan, list the
  plan(s) that `Implements:` it, each with a link and its current **status**
  (`draft` / `active` / `done` / `abandoned`) — so a human sees implementation
  progress at a glance without opening the plan file. ADRs with no
  implementing plan yet are simply absent from the sub-index (no need to
  render an empty row).
- **Regeneration.** Built the same way as the rest of `overview.md`: read every
  plan's `Implements:` field and `Status:` field, group by target ADR, and
  write the sub-index fresh as part of the normal wholesale regeneration
  (ADR-0011). It is never hand-patched and carries the same "as of" staleness
  stamp as the rest of the file.
- **Scope.** This amends only ADR-0011's definition of `overview.md`'s shape.
  ADR-0012 (no ADR→plan back-link) is explicitly left untouched — the ADR
  artifact itself gains no new field; only the derived snapshot changes.

## Consequences

- A human reading `overview.md` can answer "how was this ADR implemented?" by
  looking it up in one place, with no grep and no need to ask the agent
  (Transparency #3, Continuity #1).
- No new authoritative field is added anywhere; the sub-index is entirely
  derived from the existing `Implements:` header, so there is nothing new to
  maintain or let drift (Economy #2).
- ADR-0012's write-once-reciprocal reasoning stands unchallenged: ADRs still
  carry no plan back-link; only the regenerated `overview.md` changes shape.
- The regeneration procedure (refresh procedure in `AGENTS.md` / the working
  method) gains one more derived section to produce from the same header scan
  it already performs — a small, bounded addition, not a new pass over the
  repo.
- A plan is needed to carry this out: extend the `overview.md` template and
  the refresh procedure text (in the working-method spec and `AGENTS.md`) to
  describe and generate the ADR → plans sub-index, then regenerate
  `overview.md` once to demonstrate it.
