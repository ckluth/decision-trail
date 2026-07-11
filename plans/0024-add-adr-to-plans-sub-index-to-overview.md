# Plan 0024: add the ADR → plans sub-index to `overview.md`

- Date: 2026-07-11
- Status: done
- Implements: [ADR-0034](../decisions/0034-derived-adr-to-plans-sub-index-in-overview.md)

## Goal

Land what ADR-0034 accepted: extend `overview.md`'s shape with a derived,
regenerated **ADR → plans sub-index** — for each ADR, the plan(s) whose
`Implements:` field points to it, each with its current status
(`draft` / `active` / `done` / `abandoned`) — with no new hand-maintained field
and no back-link added to the ADR artifacts themselves.

## Tasks

### Spec sharpening (canonical)

- [x] In `starter/docs/working-method.md`, extend the `docs/overview.md`
      paragraph (§ *The lifecycle*) to describe the second, ADR-oriented view:
      after the existing "single dated snapshot of each artifact's name,
      creation date, and state" sentence, add that `overview.md` also carries a
      derived **ADR → plans sub-index**, grouping each ADR with its implementing
      plan(s) and their status, built from the same header scan.
- [x] Extend the **Refresh procedure** paragraph (same section) so the scan step
      also reads each plan's `Implements:` field and groups plans by target ADR
      to build the sub-index, alongside rewriting the three family tables.
- [x] Regenerate this repo's `AGENTS.md` **derived method body** (§ *The
      lifecycle*) from the updated canonical text, applying the standard
      deltas (repo-root paths, construction-ADR refs, no provenance citation).
      Touch nothing outside the derived section.

### Ship the scaffold

- [x] Update `starter/docs/overview.md` (the template an adopter copies) to add
      an empty **"Implements" / ADR → plans** section header beneath the three
      family tables, ready to be populated on first regeneration.

### Reconcile this repo's overview

- [x] Regenerate this repo's `overview.md` wholesale: keep the three existing
      family tables, and add the new ADR → plans sub-index populated from every
      plan's `Implements:` field currently in `plans/`, each row showing the
      plan and its status. Re-stamp "as of <date>".

### Codify the ADR-title rendering

- [x] In `starter/docs/working-method.md` and this repo's `AGENTS.md`, add a
      clause to the sub-index description pinning that each ADR row renders as
      **`ADR-000n – Title`** (link text includes the title, not just the
      number), so the format survives future regenerations instead of relying
      on memory.

## Verification

- [x] `grep` confirms the ADR → plans sub-index description appears in both
      `starter/docs/working-method.md` and this repo's `AGENTS.md` derived body,
      with consistent wording.
- [x] This repo's regenerated `overview.md` contains an ADR → plans sub-index
      entry for ADR-0034 itself, pointing at this plan (0024, `active`).
- [x] Spot-check one other ADR with multiple implementing plans (e.g. ADR-0011)
      to confirm the sub-index lists all of them with correct statuses. (No ADR
      in this repo currently has more than one plan; ADR-0011's single-plan row
      is correct.)

## Notes

- Scope is the method *text* and this repo's `overview.md` only. Cutting a
  decision-trail **release** (version bump, `CHANGELOG.md` entry with an
  `Adopter migration:` line, per ADR-0021/ADR-0022) is separate downstream work,
  not part of this plan.
- Per ADR-0034, ADR-0012 (no ADR→plan back-link) is untouched — no ADR artifact
  gains a new field; only the derived `overview.md` changes shape.
