# 2. Make the `Promoted` link reciprocal

- Status: done
- Date: 2026-06-28
- Implements: [ADR-0012](../decisions/0012-promotion-carries-a-reciprocal-promoted-from-back-link.md)

## How

ADR-0012 is the spec. Add the `Promoted from:` back-link to every existing
promotion target, record the reciprocity (and its "both ends single and
write-once" criterion) in the cross-link vocabulary of both the canonical
`AGENTS.md` and the `starter/` method text, then cut version 1.4.0.

## Tasks

- [x] Add `Promoted from: [idea 0003](...)` to ADR-0011's header.
- [x] Add `Promoted from: [idea 0002](...)` to ADR-0008's header (backfill).
- [x] Update `AGENTS.md` cross-link table: `Promoted to:` / `Promoted from:`
      become a reciprocal pair; update the "forward link always" note to include
      promotion and state the reciprocity criterion.
- [x] Update `starter/docs/working-method.md` cross-link table identically.
- [x] Add a `## [1.4.0]` entry to `CHANGELOG.md` (ADR-0012, amends ADR-0005).
- [x] Regenerate `overview.md` (ADR-0012 now accepted; re-stamp the date).
