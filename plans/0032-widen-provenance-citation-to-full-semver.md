# Plan 0032: Widen the provenance citation to vX.Y.Z across live surfaces, ship 2.19.0

- Date: 2026-07-17
- Status: done
- Implements: [ADR-0043](../decisions/0043-pin-the-provenance-citation-to-full-three-component-semver.md)

Mechanical execution of ADR-0043: pin the provenance citation to full three-component
semver (`vX.Y.Z`) across the **live** surfaces that define/describe/enforce the
citation format, and make `updating.agent.md`'s read-version step read all three
components so a patch/fix release is in scope. Ship as the **2.19.0** minor release
with a **required** migration note (re-cite with the patch component if it was
dropped). Historical prose recording the old `vX.Y` string is left as history.

## Tasks

- [x] `starter/docs/decisions/0001-adopt-decision-trail.md` — adopter template:
      "adopts decision-trail at version **vX.Y**" → **vX.Y.Z**.
- [x] `starter/docs/working-method.md` — delta note: the `Based on decision-trail
      vX.Y` provenance citation → **vX.Y.Z**.
- [x] `updating.agent.md` step 1 (read current version) — placeholder → **vX.Y.Z**
      and state it reads the **full major.minor.patch**, so a patch bump is not
      mistaken for the same version.
- [x] `updating.agent.md` conformance item #6 — placeholder → **vX.Y.Z**.
- [x] `adopting.md` — all four spots (intro breadcrumb, fresh-repo fill-in,
      update read-version, conformance description): `vX.Y` → **vX.Y.Z**.
- [x] `AGENTS.md` (this repo) — preamble delta note + conformance guidance:
      `vX.Y` → **vX.Y.Z**.
- [x] Bump the three `starter/` provenance citations v2.18.2 → **v2.19.0**
      (`starter/AGENTS.md`, `starter/docs/working-method.md`, `starter/docs/guide.md`).
- [x] Add a `CHANGELOG.md` `[2.19.0]` entry with a **required** `Adopter migration:`
      note (ensure the citation carries all three semver components in both places;
      append the patch of your current version if only major.minor is present).
- [x] Add the reciprocal `Amended by: ADR-0043` to ADR-0008.
- [x] Regenerate `overview.md` from the artifact headers.
