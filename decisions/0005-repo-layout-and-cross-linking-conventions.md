# 5. Repo layout and cross-linking conventions

- Status: accepted
- Date: 2026-06-28
- Amended by: ADR-0009 (adopters use `docs/`, not a `the-way/` folder)

## Context

ADR-0001 to ADR-0004 assigned every lifecycle stage to one of three artifact
families — `ideas/`, `decisions/`, `plans/` — created at the top level of this
repository as decisions were made. Two questions were left open by ADR-0004:
*how the repo is laid out to hold these families*, and *how the parts
cross-link*.

The layout must serve two promises that pull in slightly different directions:

- **Continuity & Economy** (#1, #2): the artifacts should be prominent and cheap
  to find — a fresh session should not hunt for them.
- **Genericity** (#7): the method must be droppable into *any* project without
  colliding with that project's own folders (a host repo may already have its
  own `plans/` or `docs/`).

The cross-links between artifacts already exist informally (an idea names its
`Parent`, a plan will name what it `Implements`, ADR-0003 amended ADR-0001). We
should fix a small, consistent, greppable vocabulary rather than let each link
phrase itself differently.

## Decision

### Layout

- The three artifact families are sibling directories: `ideas/`, `decisions/`,
  `plans/`.
- **Portability rule:** when the method is adopted *into another project*, these
  three directories live under a single root directory (default name
  `the-way/`), so they never collide with the host project's own folders
  (Genericity #7). The root name is the only thing a host project may rename.
- **In this repository** — which *is* the method's own development — the
  repository root itself plays the role of that root. The three families
  therefore sit at the top level here, and we deliberately avoid self-nesting
  them under a redundant `the-way/the-way/`.
- The contract and agent hand-off file (`.github/copilot-instructions.md`) lives
  *outside* the artifact root. It is a borrowed agent-handoff standard (#8) that
  describes the method; it is not itself a lifecycle artifact.

### Cross-linking

All cross-links are **relative markdown links** with a fixed set of field names,
written in the artifact's header so they are easy to grep:

| From | Field | To | Meaning |
|------|-------|----|---------|
| idea | `Parent:` | idea | this idea budded from another (#6) |
| idea | `Promoted to:` | ADR | this idea matured into a proposal |
| ADR | `Amends:` / `Amended by:` | ADR | a part of one ADR was changed by another |
| ADR | `Supersedes:` / `Superseded by:` | ADR | one decision replaces another |
| plan | `Implements:` | ADR | this plan carries out a decision |

- **Forward link always; reciprocal back-link for amend/supersede.** When ADR B
  amends or supersedes ADR A, B carries the forward field and A is given the
  matching back-link, so the trail is walkable from either end (Continuity #1).
  One-directional fields (`Parent`, `Promoted to`, `Implements`) need no
  reciprocal entry.

## Consequences

- The repository layout is now fixed: `ideas/`, `decisions/`, `plans/` as
  siblings, with `.github/` holding the contract. A returning session knows
  exactly where to look (Continuity #1).
- The portability rule keeps the method generic: any host project gets one
  `the-way/` root rather than three top-level folders that might clash
  (Genericity #7). This ADR is also the first place that names the default root
  directory `the-way/`.
- The link vocabulary is small and consistent; relationships across the
  lifecycle can be found with a single `grep` for the field name, with no
  tooling (Transparency #3).
- A natural follow-on remains: a single human/agent entry point (an index or
  `AGENTS.md`) that teaches the method by pointing at these families. That is a
  future decision.
