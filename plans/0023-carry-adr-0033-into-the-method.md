# Plan 0023: carry ADR-0033 into the method — author-from-spec rule + proposal heading convention

- Date: 2026-07-11
- Status: done
- Implements: [ADR-0033](../decisions/0033-author-from-the-spec-not-from-a-sibling.md)

## Goal

Land the two changes ADR-0033 accepted:

1. a new **agent-guidance rule** — *author from the spec, never from a sibling* —
   in the agent operating guidance (canonically `starter/AGENTS.md`, mirrored in
   this repo's `AGENTS.md`);
2. a **spec sharpening** — pin the `## Proposed decision` → `## Decision`
   rename-on-acceptance convention — in `starter/docs/working-method.md`, then
   regenerate this repo's derived `AGENTS.md` method body to match.

## Tasks

### Spec sharpening (canonical)

- [x] In `starter/docs/working-method.md`, extend the **Decisions** bullet
      (§ *The lifecycle*, the "classic template" line) to pin the heading
      convention: a proposal uses `## Proposed decision` while `Status: proposed`;
      on acceptance the status flips to `accepted` **and** the heading is renamed
      to `## Decision` — status and heading move together.
- [x] Regenerate this repo's `AGENTS.md` **derived method body** (§ *The
      lifecycle*, Decisions bullet) from the updated canonical text, applying the
      standard deltas (repo-root paths, construction-ADR refs, no provenance
      citation). Touch nothing outside the derived section.

### Agent-guidance rule

- [x] Add the **"author from the spec, never from a sibling"** rule to
      `starter/AGENTS.md` § *Agent operating guidance* (verbatim wording from
      ADR-0033, including the bounded format-conformance exception).
- [x] Mirror the same rule into this repo's `AGENTS.md` § *Agent operating
      guidance* (the non-derived section), phrased for this repo.

### Reconcile the index

- [x] Regenerate `overview.md` wholesale from the artifact headers (picks up idea
      0027 `promoted`, ADR-0033 `accepted`, this plan, and stamps "as of <date>").

## Verification

- [x] `grep` confirms the author-from-spec rule is present in both
      `starter/AGENTS.md` and this repo's `AGENTS.md`.
- [x] `grep` confirms the `## Proposed decision` → `## Decision` convention appears
      in `starter/docs/working-method.md` and in this repo's `AGENTS.md` derived
      body, with consistent wording.
- [x] `overview.md` rows for idea 0027, ADR-0033, and plan 0023 match their headers.

## Notes

- Scope is the method *text* only. Cutting a decision-trail **release** (version
  bump, `CHANGELOG.md` entry with `Adopter migration:` line, per ADR-0021/ADR-0022)
  is separate downstream work, not part of this plan.
- No back-migration of existing artifacts: accepted ADRs already carry
  `## Decision`, proposals already use `## Proposed decision` (ADR-0033
  Consequences).
