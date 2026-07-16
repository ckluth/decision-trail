# Delivered artifacts

This folder is decision-trail's own home for **content *created* as the output of a
plan** — a report, a spec document, a diagram: work authored fresh, rather than
*distilled* from other artifacts (ADR-0039). It is one of the optional `*-artifacts/`
companion folders, split from its neighbours by the **origin** of what it holds.

**What this is not:** it is **not a fourth lifecycle family** and **not a new source
of truth.** The ideas, decisions, and plans remain the only lifecycle sources of
truth. This folder simply gives created content a conventional home and distinguishes
it by *origin* — not by claiming special authority. Where a deliverable's existence or
shape is itself a decision, an ADR governs it (as for any work), but the folder adds
no lifecycle status and no cross-link field.

**How to use it:**

- **Guard split.** Folder *mechanics* — creating the folder, dropping this README,
  filing or moving files — are guard-free. But *creating the deliverable content* is
  real plan work and follows the **normal confirmation guard**; there is no blanket
  guard-free grant for content.
- **Internally unstructured.** Organize the contents however suits the work.
- **Committed by default**, so created work survives across machines and sessions.

Contrast with its neighbours:

- `../derived-artifacts/` — **derived** projections mechanically distilled from the
  authoritative artifacts (the ADRs). Regenerable, never a source of truth.
- `../intermediate-artifacts/` — guard-free **scratch** gathered while a plan runs;
  informal, and allowed to rot harmlessly once the plan is done.
- Delivered artifacts here — **created** work products: authored fresh as plan output.

A rule of thumb: if losing the file means *re-running a generator*, it belongs in
`derived-artifacts/`; if losing it means *re-doing creative work*, it belongs here; if
losing it costs nothing, it was `intermediate-artifacts/` scratch.

This folder currently holds no content — it stands ready for the next plan that
produces created work.
