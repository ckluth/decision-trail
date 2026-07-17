# ADR-0043: Pin the provenance citation to full three-component semver

- Date: 2026-07-17
- Status: accepted
- Promoted from: [idea 0037](../ideas/0037-citation-format-drops-the-patch-component.md)
- Amends: [ADR-0008](0008-adopt-the-way-via-a-copied-starter-skeleton.md)

## Context

decision-trail is versioned with **semver** and now ships genuine **patch releases**
(v2.18.1, v2.18.2 are both `Fixed`-type). ADR-0008 introduced the provenance citation
as a **two-component** string — *"Based on the-way vX.Y — <repo URL>"* — and every
live surface has carried that `vX.Y` placeholder since: the adopter template
(`starter/docs/decisions/0001-adopt-decision-trail.md`), the read-version step and
conformance item #6 in `updating.agent.md`, the on-ramp `adopting.md`, and the
delta-note references in `starter/docs/working-method.md` and this repo's `AGENTS.md`.

The placeholder is not just cosmetic: it advertises the **scope** at which a version
is read and compared. When a consumer reads its current version "from the
`Based on decision-trail vX.Y` citation" and models it as `X.Y`, the **patch component
falls out of scope** — a repo on `v2.18.1` and a target `v2.18.2` both collapse to
"v2.18", so a **fix-level change is not recognized**. This is a real, observed bug: a
consumer repo did not recognize a semver fix change because only major and minor were
in its scope.

The literal citations already carry the patch — all three `starter/` renderings read
`v2.18.2` — so the copied *string* is fine; the defect is that the **format the method
pins and the scope it enforces** stop at two components.

## Decision Drivers

- **Correctness over cosmetics** — a patch/fix release must be recognizable to a
  consumer; that requires the citation and its comparison to include the patch.
- **Fix at the source** — widen the pinned *format* and the read/compare *scope*, not
  bolt on a special-case for patches.
- **Cheap and copy-driven (ADR-0022)** — a placeholder/scope refinement; no new
  mechanism, no manifest; `starter/` stays the single source of truth.
- **Respect the derived-body rule (ADR-0014/0032)** — the two `AGENTS.md` edits are in
  its non-derived preamble and agent-guidance, not its regenerated method body.

## Considered Options

1. **Leave `vX.Y` as-is.** Cheapest (zero work), but preserves the exact scope defect
   that already caused a fix release to go unrecognized. Rejected.
2. **Special-case patch detection** — keep `vX.Y` but add a rule "also compare the
   patch." Two sources of truth for the version's shape; the placeholder still
   *advertises* two components. Rejected as needless complexity.
3. **Pin the citation to full three-component semver `vX.Y.Z` (chosen).** Change the
   placeholder to `vX.Y.Z` across the live surfaces, and make the read-version step
   read all three components, so patch is in scope by construction.

## Decision

Adopt option 3. **The provenance citation carries the full three-component semver,
`vX.Y.Z` (major.minor.patch), and version reading/comparison is on all three
components.**

- Replace the placeholder `vX.Y` → `vX.Y.Z` on every **live** surface that defines,
  describes, or enforces the citation format: the adopter template
  `starter/docs/decisions/0001-adopt-decision-trail.md`; `updating.agent.md`
  (read-version step **and** conformance item #6); `adopting.md` (all four spots); the
  delta-note reference in `starter/docs/working-method.md`; and this repo's `AGENTS.md`
  (preamble delta note + conformance guidance).
- Strengthen `updating.agent.md`'s read-version step so it reads the **full
  major.minor.patch**, so a patch bump is not mistaken for "the version I already
  have."
- Leave **historical prose** that merely *records* the old two-component string
  (accepted ADRs, past plans, past `CHANGELOG` entries) untouched — accepted decisions
  are never edited in place; they are history.
- This **amends ADR-0008** (the origin of the two-component citation string) in the
  component-count of the citation format only; the copy-driven adoption mechanics are
  otherwise unchanged. On acceptance, add the reciprocal `Amended by: ADR-0043` to
  ADR-0008.

Ship it as a **minor release (2.19.0)**: it broadens the citation-format contract and
requires an adopter that dropped the patch to re-cite, so it is not a pure-wording
patch. Its `CHANGELOG` migration note is **required**: ensure the citation carries all
three components in both `docs/working-method.md` and the `AGENTS.md` "How we work"
block; if it reads only `major.minor`, append the patch of the version you are on.

## Consequences

- **Fix releases are recognizable** — reading and comparing the full `vX.Y.Z` means a
  consumer on `v2.18.1` correctly sees `v2.18.2` as newer; the observed bug cannot
  recur.
- **One version shape everywhere** — the placeholder, the adopter template, the
  read-version step, and the conformance check all speak three-component semver; no
  split between "what we cite" and "what we compare."
- **ADR-0008 amended in detail only** — the citation string gains its third component;
  copy-driven adoption is otherwise unchanged. Reciprocal `Amended by: ADR-0043` added
  to ADR-0008.
- **Adopter action is small and bounded** — re-cite with the patch component if it was
  dropped; the migration note states it as executable steps. Current adopters already
  citing `v2.18.2` need only the version bump.
- **Follow-on:** on acceptance, a `draft` stub plan `Implements:` this ADR to make the
  `vX.Y` → `vX.Y.Z` edits across the live surfaces, strengthen the read-version step,
  bump the three `starter/` citations v2.18.2 → **v2.19.0**, add the `CHANGELOG`
  **2.19.0** entry with the required migration note, add the reciprocal
  `Amended by: ADR-0043` to ADR-0008, and regenerate `overview.md`.
