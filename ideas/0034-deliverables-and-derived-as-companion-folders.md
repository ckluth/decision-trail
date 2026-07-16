# Idea 0034: delivered-artifacts and derived-artifacts — two more companion folders

- Date: 2026-07-16
- Status: promoted
- Promoted to: [ADR-0039](../decisions/0039-delivered-and-derived-artifacts-companion-folders.md)

## Observation

The method already ships one **guard-free companion folder** for material that has
no home among the authoritative artifacts: `intermediate-artifacts/`
(idea 0013 → ADR-0020) — a scratch persistence layer for the execution stage. It is
little more than *a folder plus a README explaining how to use it*, and that has
proven to be enough.

The adopting repo **josyn-builder** has since grown **two more folders of the same
family**, each with its own README, living beside `intermediate-artifacts/` under
`docs/`:

- **`deliverables/`** — **authored, original work products** produced as the output
  of a plan. A deliverable is *not distilled from anything*: it is written fresh and
  **is authoritative for its own content**. You never "regenerate" a deliverable;
  you revise it (ideally under a plan), and where its existence or shape is a
  decision, an ADR governs it.
- **`derived/`** — **human-facing projections mechanically distilled** from the
  authoritative artifacts (chiefly the ADRs). Each one summarizes decisions
  otherwise scattered across many records, links back to its sources, and can be
  **regenerated on request**. A convenience, **never a source of truth** — the same
  status the existing `overview.md` status index already holds.

Both work well in josyn-builder and are, like `intermediate-artifacts/`, barely more
than a folder and a hint on how to use it. This idea asks whether they clear the bar
to become **shipped, optional companions of the method** (Borrow, don't invent #8 —
prove locally first, then promote).

## Framing

These are **working-material** members, not new lifecycle families — exactly like
`intermediate-artifacts/`, the travel diary, and the `Tags:` axis. Neither carries a
status, takes a place in the idea → proposal → decision → plan → execution flow, nor
holds cross-link fields. They sit *beside* the lifecycle as companions.

What is interesting is that the three folders form a small, coherent **material
taxonomy** distinguished by *authority and origin*:

| Folder | Authority | Origin | Lifespan |
|--------|-----------|--------|----------|
| `intermediate-artifacts/` | not a source of truth | gathered scratch | rot harmlessly |
| `derived/` | not a source of truth | mechanically distilled from ADRs | regenerated on demand |
| `deliverables/` | **authoritative for its own content** | authored fresh (plan output) | revised, kept current |

A useful rule of thumb (borrowed verbatim from the josyn-builder README): *if losing
the file means re-running a generator, it belongs in `derived/`; if losing it means
re-doing creative work, it belongs in `deliverables/`; if losing it costs nothing,
it was `intermediate-artifacts/` scratch.*

Note one subtlety worth resolving before promotion: `deliverables/` introduces the
method's **first authoritative artifact that is not an idea/decision/plan**. Every
other companion is explicitly "not a source of truth"; a deliverable *is* a source of
truth for its own content (though not a lifecycle artifact). That is a genuinely new
shape and deserves careful wording so it neither reads as a fourth lifecycle family
nor gets mistaken for disposable scratch.

## Prior art (Borrow, don't invent #8)

Both folders are already implemented and in use in **josyn-builder**, each with a
short README that positions it against its two neighbours. `derived/` there holds
real projections (e.g. a classification-vocabulary and a repo-landscape document,
each citing the ADRs it distills); `deliverables/` holds authored outputs. Promoting
them mirrors exactly how `intermediate-artifacts/` itself was promoted from
josyn-builder into the method (idea 0013 → ADR-0020).

## Candidate shape

- **Two conventional folders + names** — `delivered-artifacts/` and
  `derived-artifacts/` — at the repo root here, `docs/`-prefixed in adopters,
  mirroring the layout split of ADR-0009 and joining `intermediate-artifacts/` in one
  visibly-parallel `*-artifacts/` companion family.
- **A short README in each**, self-describing (how the folder is used and what it is
  *not*), positioned against its neighbours — adapt the josyn-builder READMEs as the
  starting text (renaming the folders to the parallel form).
- **`derived-artifacts/` = not a source of truth**, regenerable, curated and kept
  current; the topical-projection counterpart to the machine-facing `overview.md`
  status index.
- **`delivered-artifacts/` = the home for plan-*created* (not derived) content** —
  work authored fresh as plan output. The distinguishing axis across the three
  companions is **origin**: gathered scratch vs. derived/distilled vs. created. The
  method does **not** overclaim it as an authoritative lifecycle member.
- **Guard split.** Folder *mechanics* (creating the folder, dropping the README,
  filing/moving files) are guard-free like `intermediate-artifacts/` (ADR-0020) and
  the travel diary (ADR-0018); *creating deliverable content* is real plan work and
  follows the **normal confirmation guard** — no blanket guard-free grant for content.
- **Ship documented-but-empty in `starter/`**, like `intermediate-artifacts/`, since
  the *contents* are project-specific.
- **Spec + AGENTS.md coverage** — add short companion sections to
  `starter/docs/working-method.md`, regenerate the derived `AGENTS.md` body, and
  mention them in the layout and agent-guidance where the other companions appear.

## Resolutions

Worked through in conversation (2026-07-16); the idea is ready to promote:

1. **One idea or two? → one ADR** covering both folders as a companion-material
   taxonomy — their value is the *contrast between the three folders*, so a single
   decision keeps the picture whole (and the footprint minimal).
2. **The authority novelty → weaken the definition.** Don't frame
   `delivered-artifacts/` as "authoritative for its own content"; frame it plainly as
   *the place where plan-created (not derived) content has a home*. This sidesteps the
   "first authoritative non-lifecycle member" tension entirely — the three companions
   split by **origin** (gathered / derived / created), not by authority.
3. **Guard for deliverables → split.** Folder mechanics guard-free; deliverable
   *content* follows the normal confirmation guard as ordinary plan work.
4. **Relationship to `overview.md` → keep distinct, note the kinship.** `overview.md`
   stays the *special, always-present* derived status index at the root (ADR-0011);
   `derived-artifacts/` holds *optional, topical* projections. One line acknowledges
   they are both regenerated, not-a-source-of-truth projections.
5. **Regeneration bookkeeping → recommend, don't mandate.** A derived document should
   link back to the artifacts it distills (so it stays regenerable and auditable), but
   the method pins no exact format — the josyn-builder inline "Derived from ADR-00xx"
   style is the natural example, not a rule.
6. **Naming → parallel form.** Ship `delivered-artifacts/` and `derived-artifacts/`
   rather than josyn-builder's `deliverables/` and `derived/`, so all three companions
   share the `-artifacts` suffix and read as one family. The "artifact means
   authoritative" collision worry already existed for `intermediate-artifacts/` and
   was accepted in ADR-0020; extending the suffix is consistent, not newly risky.
   (Adoption renames the josyn-builder folders — a one-time migration.)
7. **Scope creep → clears the bar.** Generic recurring need + proven in real use in
   josyn-builder + fits the established `*-artifacts/` companion pattern — the same bar
   `intermediate-artifacts/`, the diary, and tags each cleared. Promote toward one ADR.
