# the-way

A generic, reusable way to work on projects — economic, transparent, agile.
This is the entry point: read it first, then navigate from here.

## What this is

`the-way` is a method for carrying a thought through its whole life, in plain
markdown, borrowing existing standards rather than inventing new ones. Its
**contract** — the eight promises it keeps — is the single source of truth and
lives in [`.github/copilot-instructions.md`](.github/copilot-instructions.md).

## The lifecycle

A thought travels: **idea → proposal → decision → plan → execution.** Each stage
has a home, across three artifact families:

| Stage | Where it lives | Status values |
|-------|----------------|---------------|
| idea | `ideas/NNNN-*.md` | `seed` → `promoted` / `dropped` |
| proposal | `decisions/NNNN-*.md` | `proposed` |
| decision | `decisions/NNNN-*.md` (same file) | `accepted` / `rejected` |
| plan | `plans/NNNN-*.md` | `draft` → `active` → `done` / `abandoned` |
| execution | `plans/NNNN-*.md` (same file) | the plan ticking its checkboxes |

- **Ideas** are cheap to write; a matured idea is *promoted* to a proposal.
- **Decisions** are [ADRs](decisions/) — a proposal *becomes* a decision in
  place when accepted.
- **Plans** carry an accepted decision into action; the ADR is the spec, the
  plan is the *how*, and execution is the plan in motion. Tasks use GitHub
  task-list markdown (`- [ ]` / `- [x]`).

## Layout

```
ideas/        idea artifacts
decisions/    proposal + decision artifacts (ADRs)
plans/        plan + execution artifacts
.github/      the contract and agent hand-off files
AGENTS.md     this entry point
```

When the method is adopted into another project, these families nest under a
single `the-way/` root to avoid colliding with the host project's folders. In
*this* repository, the repo root itself is that root.

## Cross-link vocabulary

Artifacts reference each other with relative markdown links and fixed,
greppable field names in their headers:

| From | Field | To | Meaning |
|------|-------|----|---------|
| idea | `Parent:` | idea | budded from another idea |
| idea | `Promoted to:` | ADR | matured into a proposal |
| ADR | `Amends:` / `Amended by:` | ADR | part of a decision changed |
| ADR | `Supersedes:` / `Superseded by:` | ADR | one decision replaces another |
| plan | `Implements:` | ADR | carries out a decision |

Forward link always; add the reciprocal back-link for amend/supersede so the
trail is walkable from either end.

## How to start working

1. Capture a thought as an idea in `ideas/`.
2. When it matures, open an ADR in `decisions/` with `Status: proposed`.
3. Accept or reject it; an accepted ADR is a decision.
4. Write a `plans/` file that `Implements:` the decision and lists tasks.
5. Execute by moving the plan `active` → `done`, ticking checkboxes.

## Why it is this way

Every mechanic above was decided one step at a time, each recorded as an ADR.
Read [`decisions/`](decisions/) in order to see the reasoning — the method
documents its own construction.
