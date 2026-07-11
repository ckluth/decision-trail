# Plan 0018: pin the title-line format so the ordinal is always visible in the H1

- Date: 2026-07-11
- Status: done
- Implements: [ADR-0028](../decisions/0028-pin-the-title-line-format-ordinal-in-h1.md)

## Goal

Carry [ADR-0028](../decisions/0028-pin-the-title-line-format-ordinal-in-h1.md)
into the method texts and this repo's own artifacts. The title line (H1) had no
stated format and drifted into two schemes per family, diverging across all
three families — the same class of bug as ADR-0025 (numbering) and ADR-0026
(header rendering): a convention living as folklore, not a stated, checkable
rule. Fix it by (a) **stating the canonical title-line template** (typed +
zero-padded, ordinal echoes the filename slot) in the method texts, (b)
**hardening the refresh procedure** to match the pinned form, (c) **adding a
title↔filename ordinal-match check** to the conformance check (ADR-0022,
alongside the ADR-0025/ADR-0026 steps), and (d) **sweeping every existing
artifact** in this repo to the canonical form in one pass. Close sibling of
ADR-0025 / plan 0015 and ADR-0026 / plan 0016; keep both renderings in sync
(ADR-0014) and ship as a release whose behavioral migration is "none" (the
wording reaches adopters via the copy-driven "bring me current" update,
ADR-0022).

## Tasks

- [x] **Canonical method body — title-line template.** In
      `starter/docs/working-method.md`, near the existing header-block template
      (added by ADR-0026), state the canonical **title-line** form: typed +
      zero-padded, ordinal echoes the filename slot, family named —
      `# Idea 0017: Title`, `# ADR-0017: Title`, `# Plan 0017: Title`. Note the
      filename stays authoritative (ADR-0015); the H1 number is a visible echo,
      not a second source of truth.
- [x] **Canonical agent guidance bullet.** Add/adjust a bullet in the "Agent
      operating guidance" list of `starter/AGENTS.md` (and the repo-root
      `AGENTS.md`) stating the title-line rule and cross-referencing ADR-0028,
      next to the existing header-format bullet (ADR-0026).
- [x] **Confirm the `starter/` exemplar matches.** Check the seed ADR
      (`starter/docs/decisions/0001-adopt-decision-trail.md`) uses the canonical
      title-line form; fix if not.
- [x] **Harden the refresh procedure wording.** Update the "Refresh procedure"
      text wherever it appears (`starter/docs/working-method.md`'s lifecycle
      section, and the repo-root `AGENTS.md`'s non-derived "Agent operating
      guidance" copy) from the generic "scan for `# N. Title`" to the pinned
      form, and state the new check: if the H1 ordinal and the filename ordinal
      disagree, treat it as a conformance failure rather than silently trusting
      either one.
- [x] **Conformance check — title↔filename ordinal match.** In `adopting.md`,
      add a step to the "Conformance check" list: every artifact's H1 ordinal
      must equal its filename ordinal and name its family (`Idea`/`ADR`/`Plan`);
      flag and fix any mismatch. Site it beside the ADR-0025 duplicate-number and
      ADR-0026 header-format steps.
- [x] **Sweep this repo's artifacts — one pass, all three families.** Rewrite the
      H1 of every file in `ideas/`, `decisions/`, and `plans/` to the canonical
      form (`# Idea NNNN: Title`, `# ADR-NNNN: Title`, `# Plan NNNN: Title`),
      preserving each title's text and the filename's ordinal exactly. (Most
      decisions already conform, 0015–0028; ideas and plans need a full sweep.)
- [x] **Regenerate the derived rendering.** Regenerate the method body of the
      repo-root `AGENTS.md` from `starter/docs/working-method.md` (section
      `## The contract` through `## How to start working`), applying the
      standard deltas (repo-root paths, construction-ADR refs, no provenance
      citation), carrying the title-line template + hardened refresh-procedure
      wording there too. Do **not** touch the preamble or the non-derived
      guidance framing.
- [x] **Provenance bump.** Bump the `Based on decision-trail vX.Y` citation to
      the next minor version in both `starter/` renderings
      (`starter/docs/working-method.md`, `starter/docs/guide.md`) and the
      adopter hand-off `starter/AGENTS.md`.
- [x] **CHANGELOG + release.** Add the ADR-0028 entry to `CHANGELOG.md`'s next
      `## [x.y.0]` release (canonical title-line template + hardened refresh
      procedure + title↔filename conformance step), with **`Adopter migration:
      none`** (existing adopter artifacts keep working; adopters may optionally
      run the new conformance check and adopt the pinned title style going
      forward).
- [x] **Regenerate `overview.md`** after all edits are done (idea 0024 already
      `promoted`, ADR-0028 already `accepted`; update this plan's own state to
      `done` and reflect the new ADR-0028 row already added).
