# 4. Updating an adopted the-way in a consuming repo should be as easy as possible

- Status: seed
- Date: 2026-06-28

## Idea

When a project has adopted the-way at some version and a newer version is
released, pulling the new version into the consuming repo should be as cheap and
low-risk as it can be. Ideally the adopting agent has to do **nothing**; at most
it should follow a small, clearly stated set of migration steps.

The trigger for this thought: going from 1.2.0 to 1.3.0 is *not* a no-op for an
adopter. 1.3.0 makes a `Date:` header field mandatory on ideas and plans (and
adds `overview.md` plus the reciprocal `Promoted from:` link). An adopter that
already has idea and plan files must **insert/backfill the `Date:` fields**,
create the first `overview.md`, and may want to add `Promoted from:` back-links —
otherwise its artifacts no longer match the method it cites.

So a release can carry *adopter-facing migration work*, and right now nothing
tells the adopter what that work is.

## Why it matters

- **Economy (#2) / Continuity (#1):** taking a newer the-way should be a clean,
  bounded operation, not an archaeology project across the adopter's files.
- The method is "settled, not frozen" — versions *will* keep coming, so the
  upgrade path is a recurring cost worth minimizing once.

## Open questions (for the promoted ADR to settle)

- Where do per-version migration notes live — a `MIGRATING.md`, a section per
  release in `CHANGELOG.md`, or a `migrations/` family?
- Can/should the agent perform the migration automatically (e.g. "backfill all
  missing `Date:` fields, then regenerate `overview.md`"), and how is that
  triggered?
- How does an adopter know *which* version it is on and *which* steps apply
  between its version and the target (the `Based on the-way vX.Y` citation is the
  anchor)?
- What is the contract for a release author: must every release state its
  adopter-facing migration (even if "none")?
