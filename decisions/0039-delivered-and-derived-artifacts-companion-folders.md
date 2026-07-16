# ADR-0039: delivered-artifacts and derived-artifacts — two more companion folders

- Date: 2026-07-16
- Status: accepted
- Promoted from: [Idea-0034](../ideas/0034-deliverables-and-derived-as-companion-folders.md)

## Context

Idea 0034 observed that the method already ships one **guard-free companion folder**
for material that has no home among the authoritative artifacts:
`intermediate-artifacts/` (idea 0013 → ADR-0020), a scratch persistence layer for
the execution stage. It is little more than *a folder plus a README explaining how to
use it*, and that has proven to be enough.

The adopting repo **josyn-builder** has since grown **two more folders of the same
family**, each with its own README, living beside `intermediate-artifacts/` under
`docs/`:

- a **deliverables** folder — the home for content *created* as the output of a plan
  (a report, a spec document, a diagram), written fresh rather than distilled from
  anything;
- a **derived** folder — human-facing **projections mechanically distilled** from the
  authoritative artifacts (chiefly the ADRs), each summarizing decisions otherwise
  scattered across many records, linking back to its sources, and regenerable on
  request.

Both work well in josyn-builder and are, like `intermediate-artifacts/`, barely more
than a folder and a hint on how to use it. This ADR promotes the pair into
decision-trail (Borrow, don't invent #8 — prove locally, then promote), exactly as
`intermediate-artifacts/` itself was promoted from josyn-builder (ADR-0020).

The three folders form a small, coherent **material taxonomy** distinguished by the
**origin** of what they hold — *not* by authority:

| Folder | Origin of contents | Lifespan |
|--------|--------------------|----------|
| `intermediate-artifacts/` | **gathered** scratch | rot harmlessly |
| `derived-artifacts/` | **derived** — distilled from ADRs | regenerated on demand |
| `delivered-artifacts/` | **created** — authored as plan output | revised, kept current |

## Decision drivers

- **Economy (#2):** add as little as possible — two conventional folders, no new
  lifecycle stage, no new cross-link fields, no bookkeeping.
- **Transparency (#3):** plain files in plainly-named folders; nothing hidden.
- **Genericity (#7):** the needs ("plan-created content needs a home" and "distilled
  projections need a home") are generic, not project-specific; the method ships the
  mechanism, not the contents.
- **Borrow, don't invent (#8):** lift two concepts already proven in josyn-builder,
  and reuse the companion pattern already established for `intermediate-artifacts/`
  and the travel diary.
- **Do not corrupt the source of truth (ADR-0011):** the ideas/decisions/plans stay
  the only lifecycle sources of truth. `derived-artifacts/` is explicitly
  non-authoritative and may drift harmlessly; `delivered-artifacts/` is defined by
  *origin* (created, not derived), deliberately **without** framing it as a new
  authoritative lifecycle member.

## Considered options

1. **Guide-only tip.** Cheapest; keeps the method minimal. Rejected for the same
   reason as ADR-0020's option 1: it leaves the concepts **unnamed and unlocated**,
   so every adopter reinvents where created and derived material live — and the
   material risks leaking into `plans/` or being mistaken for authoritative. The value
   is a name, a conventional home, and an explicit statement of what each is *not*.
2. **Two explicit, optional, informal companion folders (chosen).** Mirror the
   `intermediate-artifacts/` pattern: name them, locate them, state what they are and
   are not, keep the folder mechanics guard-free. Closes the gap at minimal cost and
   completes a visibly-parallel `*-artifacts/` family.
3. **Promote as two separate ADRs (one per folder).** Rejected: their value is the
   *contrast between the three folders* (origin: gathered / derived / created); a
   single ADR keeps the taxonomy whole and the footprint minimal. Splitting would
   force each half to re-explain the family.
4. **Frame `delivered-artifacts/` as a new authoritative artifact.** Rejected as
   over-reach. It would introduce the method's first authoritative-yet-non-lifecycle
   member and strain the "the three families are the only sources of truth" framing
   every other companion leans on. Instead the definition is **weakened**:
   `delivered-artifacts/` is simply *the place where plan-created (not derived)
   content has a home* — distinguished from its neighbours by origin, not authority.
5. **Reframe `overview.md` as the canonical derived document.** Rejected: `overview.md`
   is a *special, always-present* derived **status index** over all three families,
   living at the `docs/` root by convention (ADR-0011). Folding it into
   `derived-artifacts/` would break that role. The two stay distinct; their kinship
   (both regenerated, neither a source of truth) is noted in one line.

### Naming: the parallel `*-artifacts/` form

josyn-builder named its folders `deliverables/` and `derived/`. This ADR ships them
as **`delivered-artifacts/`** and **`derived-artifacts/`** so all three companions
share the `-artifacts` suffix and read as one family of "material that is not a
lifecycle artifact." The "artifact means authoritative" collision worry already
existed for `intermediate-artifacts/` and was accepted in ADR-0020; extending the
same suffix is consistent, not newly risky. Adoption renames the josyn-builder
folders — a one-time migration.

## Decision

Introduce **delivered-artifacts** and **derived-artifacts** as two optional, informal
companion folders, joining `intermediate-artifacts/` in a parallel `*-artifacts/`
family. The distinguishing axis is the **origin** of the contents — *gathered*
(intermediate), *derived* (distilled from ADRs), *created* (authored as plan output).

- **Two conventional folders, `delivered-artifacts/` and `derived-artifacts/`.** Repo
  root here; `docs/`-prefixed in adopters (mirroring the layout split of ADR-0009).

- **`delivered-artifacts/` — the home for plan-*created* content.** Work authored
  fresh as the output of a plan (a report, a spec document, a diagram), as opposed to
  material *distilled* from other artifacts. The method does **not** frame it as a new
  authoritative lifecycle member; it names and locates a home for created content and
  distinguishes it from its neighbours by origin. Where a deliverable's existence or
  shape is itself a decision, an ADR governs it — as for any work — but the folder
  itself adds no lifecycle status and no cross-link field.

- **`derived-artifacts/` — the home for distilled projections.** Human-facing
  documents mechanically distilled from the authoritative artifacts (chiefly the
  ADRs), each summarizing decisions otherwise scattered across records. **Not a source
  of truth** — a convenience, regenerable on request when its sources change; curated
  and kept current. A derived document **should link back to the artifacts it
  distills** (so it stays regenerable and auditable); the method **recommends** this
  back-linking but **mandates no fixed format** — the inline "Derived from ADR-00xx"
  style used in josyn-builder is a natural example, not a rule.

- **Distinct from `overview.md`, kinship noted.** `overview.md` remains the *special,
  always-present* derived **status index** over all three families at the `docs/` root
  (ADR-0011). `derived-artifacts/` holds *optional, topical* projections. Both are
  regenerated, not-a-source-of-truth projections — that is their only kinship; their
  roles do not merge.

- **Guard split.** Folder **mechanics** — creating the folder, dropping the README,
  filing or moving files — are **guard-free**, like `intermediate-artifacts/`
  (ADR-0020) and the travel diary (ADR-0018). But **creating deliverable content** is
  real plan work and follows the **normal confirmation guard** — there is no blanket
  guard-free grant for the content of `delivered-artifacts/`. Regenerating a
  `derived-artifacts/` document is user-triggered (you ask for it), like `overview.md`.

- **Internally unstructured.** The method defines only *where* each folder lives and
  *what it is / is not*; the shape and organization of its contents are the project's
  business.

- **Optional and safe to ignore.** Like `intermediate-artifacts/`, the travel diary,
  and the `Tags:` axis, a repo that needs neither folder simply has none.

- **The method ships the mechanism documented-but-empty.** The `starter/` skeleton
  carries `docs/delivered-artifacts/` and `docs/derived-artifacts/` folders, each with
  a short `README` explaining its purpose and positioning it against its neighbours
  (adapted from the josyn-builder READMEs, renamed to the parallel form) — no
  fabricated contents, like the empty `Tags:` vocabulary (ADR-0017).

The method spec (`starter/docs/working-method.md`, rendered per ADR-0014) documents
these in short **Delivered artifacts** and **Derived artifacts** sections and adds the
two folders to the layout. The agent operating guidance notes the guard split.

This is additive and safe to ignore: a repo with neither folder behaves exactly as
today, and nothing in the lifecycle, overview, or cross-link vocabulary changes.

## Consequences

- The method gains two more optional **companions**, completing a visibly-parallel
  `*-artifacts/` family (`intermediate-artifacts/`, `delivered-artifacts/`,
  `derived-artifacts/`) split by origin — gathered, created, derived.
- The source of truth is untouched (ADR-0011): `derived-artifacts/` is explicitly
  non-authoritative and drifts harmlessly; `delivered-artifacts/` is defined by origin
  rather than promoted to an authoritative lifecycle member, so the "three families
  are the sources of truth" framing is preserved.
- The lifecycle, artifact families, and cross-link vocabulary are unchanged. No new
  status, verb, or field is added.
- The confirmation guard is widened only for **folder mechanics**; deliverable
  *content* keeps the normal guard, and derived regeneration stays user-triggered.
- `overview.md` keeps its distinct role as the always-present derived status index;
  `derived-artifacts/` holds optional topical projections beside it.
- The `starter/` skeleton gains `docs/delivered-artifacts/` and
  `docs/derived-artifacts/` folders, each with a purpose `README`; adopters get
  ready-made homes for created and derived material, reaching them automatically via
  the copy-driven update (ADR-0022).
- On acceptance, a plan will: add the **Delivered artifacts** and **Derived
  artifacts** sections and layout entries to `starter/docs/working-method.md` (bumping
  the provenance citation); regenerate this repo's `AGENTS.md` method body and add the
  guard-split note to the agent guidance (mirrored in `starter/AGENTS.md`); add a
  one-line mention to both `guide.md` renderings; ship the two `starter/docs/…/README`
  files; optionally seed this home repo's own `delivered-artifacts/` and
  `derived-artifacts/` folders; add a CHANGELOG entry (with an `Adopter migration:`
  line covering the josyn-builder folder rename); and regenerate `overview.md`.
