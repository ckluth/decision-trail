# Plan 0028: ship delivered-artifacts and derived-artifacts as optional companion folders

- Date: 2026-07-16
- Status: done
- Implements: [ADR-0039](../decisions/0039-delivered-and-derived-artifacts-companion-folders.md)

## Goal

Ship **delivered-artifacts** and **derived-artifacts** — two optional, informal
companion folders that join `intermediate-artifacts/` in a parallel `*-artifacts/`
family, split by the **origin** of their contents: *gathered* (intermediate),
*created* (delivered), *derived* (distilled from ADRs). Ship the **mechanism +
documented-but-empty starter folders**; the home repo may seed its own.

Per ADR-0039: `delivered-artifacts/` is the home for plan-*created* content (defined
by origin, **not** framed as a new authoritative lifecycle member);
`derived-artifacts/` holds distilled projections (**not a source of truth**,
regenerable, back-linking to sources **recommended, not mandated**). Folder mechanics
are guard-free; deliverable *content* follows the normal confirmation guard;
`derived-artifacts/` regeneration is user-triggered. Both are distinct from
`overview.md` (the always-present derived status index), kinship noted in one line.

## Design notes (placement)

- The **mechanism** (what each is, where it lives, what it is / is not) is generic
  method text → documented in `starter/docs/working-method.md` (canonical) and
  rendered into this repo's `AGENTS.md` per ADR-0014 (repo-root deltas:
  `delivered-artifacts/` and `derived-artifacts/` at root here vs.
  `docs/…` in adopters).
- The `starter/` skeleton ships `docs/delivered-artifacts/README.md` and
  `docs/derived-artifacts/README.md` explaining each folder's purpose and positioning
  it against its two neighbours (adapted from the josyn-builder READMEs, renamed to
  the parallel form; no fabricated contents), like the empty `Tags:` vocabulary.
- The guard split is noted in the **agent operating guidance** (this repo's
  `AGENTS.md` and `starter/AGENTS.md`).

## Tasks

### Method spec (canonical)
- [x] Add a **## Delivered artifacts (optional companion)** section to
      `starter/docs/working-method.md`: the home for plan-*created* (not derived)
      content; lives in `docs/delivered-artifacts/`; defined by **origin** not
      authority (explicitly not a new authoritative lifecycle member); outside the
      lifecycle and cross-link vocabulary; **folder mechanics guard-free** but
      **creating deliverable content follows the normal confirmation guard**;
      internally unstructured; optional.
- [x] Add a **## Derived artifacts (optional companion)** section to
      `starter/docs/working-method.md`: human-facing projections mechanically
      distilled from the ADRs; lives in `docs/derived-artifacts/`; **not a source of
      truth**, regenerable on request, curated/kept current; a derived document
      **should link back to the artifacts it distills** (recommended, no mandated
      format — the "Derived from ADR-00xx" style is a natural example); **distinct
      from `overview.md`** (the always-present derived status index) with the kinship
      noted in one line; outside the lifecycle; optional.
- [x] Add `docs/delivered-artifacts/` and `docs/derived-artifacts/` to the **Layout**
      block in `starter/docs/working-method.md`, positioned beside
      `docs/intermediate-artifacts/` so the `*-artifacts/` family reads together.
- [x] Bump the provenance citation to **v2.17** in `starter/docs/working-method.md`,
      `starter/docs/guide.md`, and `starter/AGENTS.md`.

### Starter skeleton
- [x] Create `starter/docs/delivered-artifacts/README.md` — a short purpose note:
      what the folder is (home for plan-created content), what it is *not* (not
      derived/distilled, not disposable scratch, not a new lifecycle family),
      positioned against its two neighbours; guard split noted; internal shape is the
      project's business. Adapt the josyn-builder text, renamed to the parallel form.
      No fabricated contents.
- [x] Create `starter/docs/derived-artifacts/README.md` — a short purpose note: what
      the folder is (distilled projections from the ADRs), what it is *not* (not a
      source of truth), regenerable on request, back-link to sources recommended,
      distinct from `overview.md`; positioned against its two neighbours. Adapt the
      josyn-builder text, renamed to the parallel form. No fabricated contents.

### Derived renderings (this repo)
- [x] Regenerate the derived method body in `AGENTS.md` (this repo) to include the
      **## Delivered artifacts** and **## Derived artifacts** sections and the two
      layout entries — applying ADR-0014 repo-root deltas (`delivered-artifacts/` and
      `derived-artifacts/` at root here).
- [x] Add the **guard-split** note (folder mechanics guard-free; deliverable content
      under the normal guard; derived regeneration user-triggered) to the **Agent
      operating guidance** in this repo's `AGENTS.md`, and mirror it in
      `starter/AGENTS.md`.

### Guides
- [x] Add a one-line mention of the two new companions (completing the `*-artifacts/`
      family alongside `intermediate-artifacts/`) near the relevant section in
      `guide.md` and `starter/docs/guide.md`.

### Home-repo dogfood (optional)
- [x] Optionally seed this repo's own `delivered-artifacts/` and `derived-artifacts/`
      folders, each with a `README.md` (same purpose notes), so the home repo has
      ready homes.

### Release
- [x] Add a `[2.17.0]` entry to `CHANGELOG.md` (Added: ADR-0039 — delivered-artifacts
      and derived-artifacts as optional companion folders; minor/additive bump) with
      an **`Adopter migration:`** line: adopters using the josyn-builder folder names
      rename `docs/deliverables/` → `docs/delivered-artifacts/` and `docs/derived/` →
      `docs/derived-artifacts/`; adopters without them get the empty starter folders
      automatically via the copy-driven update.

### Overview
- [x] Regenerate `overview.md` to include idea 0034, ADR-0039, and this plan; rebuild
      the ADR → plans sub-index and the ADR — stand-alone decision list; restamp "as of".

## Out of scope

- Any authoritative *lifecycle* role for delivered-artifacts — it is a home for
  created content defined by origin, not a fourth source-of-truth family, and no
  formal cross-link field is added.
- A mandated format for derived-document source citations — back-linking is
  recommended, its rendering left to the project.
- Reframing `overview.md` as a derived-artifacts document — it stays the distinct,
  always-present status index.
- A prescribed internal structure for either folder — organization is left to the
  project.
