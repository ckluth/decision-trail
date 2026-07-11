# ADR-0002: Capture an idea as a small markdown file

- Status: accepted
- Date: 2026-06-28

## Context

The lifecycle of a thought runs idea → proposal → decision → plan → execution
(promise #4). ADR-0001 gave the **decision** stage a home (`decisions/`). The
**idea** stage — the lifecycle's entry point — still has none.

An idea-capture mechanism has to honour several promises:

- **Economy** (#2): an idea must be *cheap to write*, or it won't get written
  down at all. The shape must be minimal.
- **Transparency** (#3): the idea must be plain, in-repo markdown — not hidden
  inside an external tool such as a GitHub Issue.
- **Budding** (#6): one idea can spawn another, and the parent→child link must
  be kept.
- **Lifecycle** (#4): there must be a clear hand-off from a matured idea to the
  next stage (a proposal).
- **Borrow, don't invent** (#8): rather than design a new file format, we reuse
  the ADR pattern already established in ADR-0001.

## Decision

We capture each idea as one small markdown file.

- Ideas live in the top-level `ideas/` directory.
- Each idea is a file named `NNNN-kebab-case-title.md`, using the same numbering
  convention as ADRs (ADR-0001) — one consistent borrowed pattern, not a second
  invention.
- An idea has a deliberately minimal shape:
  - a title,
  - a **Status**: one of `seed`, `promoted`, or `dropped`,
  - an optional **Parent**: a link to the idea it budded from, e.g.
    `Parent: ideas/0003-some-earlier-idea.md`,
  - a free-form body — whatever is enough to not lose the thought.
- **Budding** (#6) is recorded by the child idea's `Parent` line.
- **Hand-off to the next stage**: when a `seed` matures it is *promoted* to a
  proposal — a new ADR opened with `Status: proposed` (per ADR-0001). The idea's
  status then becomes `promoted`, with a link to that ADR. The idea file is left
  in place; it is never deleted.

## Consequences

- The lifecycle now has two of its five stages assigned a mechanism: **idea**
  (`ideas/`) and **decision** (`decisions/`). The **proposal** stage is
  currently expressed as an ADR in the `proposed` status; whether it deserves a
  richer mechanism is a future decision. **Plan** and **execution** remain
  unassigned.
- Idea and decision artifacts share one naming convention, so a returning
  session learns the pattern once and reads both directories the same way.
- Choosing in-repo markdown over GitHub Issues keeps every stage transparent and
  tool-independent, at the cost of not using Issues' built-in workflow features —
  an acceptable trade for promises #3 and #8.
- Ideas are append-only like ADRs: a dropped idea stays as a record
  (`Status: dropped`), preserving the trail (Agility, #5).
