# Derived artifacts

This folder holds **derived documents** — human-facing projections mechanically
distilled from the authoritative artifacts (chiefly the ADRs under
`../decisions/`). Each one summarizes decisions that are otherwise scattered across
many records, links back to its sources, and can be **regenerated on request** when
those sources change. It is one of decision-trail's optional `*-artifacts/` companion
folders.

**What this is not:** derived documents are a convenience, **never a source of
truth.** To change a rule, amend the relevant ADR (write a new amending ADR — never
edit an accepted one in place), then ask for the affected derived document to be
regenerated. They sit outside the lifecycle and cross-link vocabulary and may drift
harmlessly if left stale.

**How to use it:**

- **Cite your sources (recommended).** A derived document *should* link back to the
  artifacts it distills, so it stays regenerable and auditable. The exact rendering is
  the project's business — an inline "Derived from ADR-00nn" note is a natural example,
  not a mandated format.
- **User-triggered regeneration.** Like `../overview.md`, a derived document is
  regenerated when you ask for it.

This is distinct from two neighbours:

- `../overview.md` — the derived *status index* of the whole trail (the special,
  always-present projection, living at the `docs/` root by convention). Derived
  documents here are *optional, topical* projections beside it; their roles do not
  merge.
- `../intermediate-artifacts/` — guard-free *scratch* gathered during plan execution;
  informal, not derived from anything, and allowed to rot harmlessly. Derived
  documents here, by contrast, are curated and kept current.
- `../delivered-artifacts/` — **created** work products authored fresh as plan output.
  Derived documents here are *distilled*, not authored fresh.

This folder currently holds no derived documents — it stands ready for the first
projection a project needs.
