# Idea 0037: The vX.Y citation format drops the patch component, so fix releases fall out of scope

- Date: 2026-07-17
- Status: promoted
- Promoted to: [ADR-0043](../decisions/0043-pin-the-provenance-citation-to-full-three-component-semver.md)

## The itch

decision-trail is versioned with **semver** (three components: major.minor.patch),
and the method now genuinely ships **patch releases** — v2.18.1 and v2.18.2 are both
`Fixed`-type releases. But the provenance-citation format is pinned everywhere as a
**two-component** placeholder: `Based on decision-trail vX.Y`. That template — and the
scope it implies — only reasons about *major.minor*.

The consequence bites at the consumer end. When an agent (or a human) "reads the
adopter's current version from the `Based on decision-trail vX.Y` citation" and models
it as `X.Y`, the **patch component is out of scope**. A repo on `v2.18.1` and the
target `v2.18.2` both collapse to "v2.18" — so a **fix-level change is invisible**:
the consumer repo does not recognize that it is behind by a patch. The bug surfaced
exactly this way — a fix change was not recognized because only major and minor were
in scope.

## The fix framing

The citation must carry the **full three-component semver**, `vX.Y.Z`, and version
comparison / conformance must be on all three components so a patch/fix release is
recognizable. The placeholder is stamped across the *live* surfaces that define,
describe, or enforce the citation format:

- the adopter template `starter/docs/decisions/0001-adopt-decision-trail.md`
  ("adopts decision-trail at version vX.Y");
- `updating.agent.md` — the read-current-version step **and** conformance-check
  item #6;
- `adopting.md` — the human on-ramp (four spots);
- the canonical spec's delta note in `starter/docs/working-method.md`;
- this repo's `AGENTS.md` (preamble delta note + conformance guidance).

The actual *literal* citations already carry the patch (all three `starter/`
renderings read `v2.18.2`) — so the string an adopter copies is not the problem; the
**format/scope the placeholder advertises** is. Widen the placeholder to `vX.Y.Z`
everywhere it is live, and make the read-version step explicitly read all three
components.

## Directions to weigh (for the proposal, not this seed)

- Change the placeholder `vX.Y` → `vX.Y.Z` across the live surfaces only; leave
  historical artifact/CHANGELOG prose that merely *records* the old string as history.
- Strengthen `updating.agent.md`'s read-version step so it reads the full
  major.minor.patch, so a patch bump is not mistaken for "same version."
- Whether this amends the citation-format origin (ADR-0008) or the conformance
  contract (ADR-0022) — likely amends ADR-0008, which set the two-component
  `Based on the-way vX.Y` string.
- Release shape: a fix that also broadens the citation-format contract and requires
  adopters to re-cite with the patch component if they dropped it — likely a **minor**
  bump with a *required* migration note, not a pure-wording patch.

## Boundaries this must respect

- **Copy-driven contract (ADR-0022).** `starter/`'s contents stay the single source of
  truth; no manifest, no new mechanism.
- **Derived-body rule (ADR-0014/0032).** `AGENTS.md`'s method body is regenerated from
  `starter/docs/working-method.md`; the two touched `AGENTS.md` lines are the preamble
  delta note and the agent-operating-guidance section — both **non-derived** and edited
  directly.
