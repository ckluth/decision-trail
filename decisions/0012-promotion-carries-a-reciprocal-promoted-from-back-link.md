# 12. Promotion carries a reciprocal `Promoted from:` back-link

- Status: accepted
- Date: 2026-06-28
- Amends: ADR-0005 (makes `Promoted to:` reciprocal, like amend/supersede)

## Context

ADR-0005 fixed the cross-link vocabulary and split it in two: amend/supersede
links carry a **reciprocal back-link** so the trail is "walkable from either end
(Continuity #1)", while the one-directional fields — `Parent`, `Promoted to`,
`Implements` — carry only a forward link and "need no reciprocal entry."

Using the method surfaced a gap in that split. When an idea is promoted, the
idea gains `Promoted to: ADR-NNNN`, but the ADR carries no structural link back
to its founding idea. A reader who opens the ADR cold cannot cheaply reach the
idea it grew from — they must grep the `ideas/` directory for the matching
`Promoted to:`. That is precisely the "walk from either end" need that justified
reciprocal links for amend/supersede, now appearing for promotion.

### Decision drivers

- **Continuity (#1):** opening an ADR should let you reach its origin idea
  without a search — the same argument ADR-0005 already accepted for
  amend/supersede.
- The usual cost of a reciprocal link — **drift between two fields that must
  stay in sync** — is near zero here: an idea promotes to exactly one ADR, once,
  and the relationship never changes afterward. The back-link is write-once.
- The cost that remains is one extra field to write at promotion time, against
  the original "need no reciprocal entry" economy of ADR-0005.

The write-once nature removes the drift risk that made forward-only attractive,
so the Continuity gain dominates.

## Decision

`Promoted to:` becomes a **reciprocal** link, like `Amends`/`Supersedes`.

- An idea keeps its forward `Promoted to: ADR-NNNN`.
- The ADR gains a matching `Promoted from: [idea NNNN](...)` header field
  pointing back to the founding idea.
- The cross-link table in the working-method text is updated: `Promoted to:` /
  `Promoted from:` move into the "reciprocal back-link" group alongside
  amend/supersede; `Parent` and `Implements` remain one-directional.

`Parent` (idea→idea) and `Implements` (plan→ADR) are left forward-only — and the
distinction follows a single principle:

> **A link is made reciprocal only when *both* ends are single and write-once.**

- *Promotion*: an idea promotes to exactly one ADR, and that ADR grew from
  exactly one idea — both ends single, fixed at promotion time → reciprocal.
- *Implements*: a plan implements one ADR, but an ADR may gain **many** plans
  over time; the back-link side would grow and need re-editing → forward-only.
- *Parent*: a child idea has one parent, but a parent may bud **many** children;
  the back-link side would grow → forward-only.

So the carve-out is not "promotion is special" but "promotion is the one link
whose reverse never accumulates." Future links are classified the same way.

## Consequences

- The idea → proposal hand-off is walkable from both ends: an ADR names the idea
  it grew from, an idea names the ADR it became (Continuity #1).
- One small, write-once field is added at promotion time; because the link never
  changes after promotion, it cannot drift out of sync, so the duplication is
  effectively free.
- ADR-0005's cross-link vocabulary is amended; the working-method table is the
  single place the change is recorded, keeping the two link groups consistent.
- Both existing promotion targets are backfilled with a `Promoted from:` link so
  the record is uniform from the start: **ADR-0011** (from idea 0003) and
  **ADR-0008** (from idea 0002). No other ADR was promoted from an idea.
- This is a use-phase refinement of the method, made the-way as a proposed ADR.
  Ships in the next version (`CHANGELOG.md`).
