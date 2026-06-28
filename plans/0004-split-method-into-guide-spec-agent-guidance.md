# 4. Split the method text into guide / spec / agent guidance, and single-source the spec

- Status: done
- Date: 2026-06-28
- Implements: [ADR-0014](../decisions/0014-sync-method-renderings-and-separate-audiences.md)

## How

ADR-0014 is the spec. It decides three things to carry out:

1. **One canonical spec, one derived rendering.** The lean spec
   `starter/docs/working-method.md` is **canonical**; this repo's `AGENTS.md`
   method body is a **derived rendering** of it, produced by applying a fixed set
   of deltas and regenerated wholesale — never hand-patched (the `overview.md`
   discipline, ADR-0011, applied to prose).
2. **Three registers.** Split today's blended method text into a didactic human
   **Guide**, a lean **Reference/spec**, and an **agent operating guidance** block.
3. **Close the adopter gaps.** Adopters receive both the Guide and the
   agent-guidance block.

Guiding principle for *what* to change: **touch live, forward-facing method
surfaces; leave history intact.** Past ideas, ADRs, and plans are dated records
and are not rewritten.

The **enumerated deltas** (the only legitimate differences between the canonical
spec and this repo's derived `AGENTS.md` rendering), to be recorded in the
canonical file's header note:
- artifact paths — repo-root families here (`ideas/`, `decisions/`, `plans/`) vs
  `docs/`-prefixed in an adopter;
- construction-ADR cross-references (`ADR-00NN`) present in this repo's rendering,
  absent in the adopter's;
- the `Based on decision-trail vX.Y` provenance citation, adopter-only;
- entry-point framing — this repo: `AGENTS.md` carries the text; adopter:
  `AGENTS.md` points to `docs/working-method.md`.

## Tasks

### Author the canonical spec (the generic, adopter-facing shape)
- [x] Write `starter/docs/working-method.md` as the **lean Reference/spec**:
      contract, lifecycle, layout, cross-link vocabulary, rules, how to start —
      terse and greppable, with the motivating prose removed (it moves to the
      Guide).
- [x] Add a **header sync note** to `starter/docs/working-method.md` declaring it
      *canonical*, and listing the enumerated deltas above.

### Author the human Guide
- [x] Write `starter/docs/guide.md` — the didactic newcomer manual: the idea told
      well, the vocabulary explained in prose, the rules narrated, in a suitable
      teaching order. It links to `working-method.md` (spec) and to the
      agent-guidance block; it duplicates neither. It teaches *using* the method
      (no decision-trail origin story).

### Split out agent operating guidance
- [x] Extract the agent-only rules (confirmation guard, "keep `overview.md`
      current", "the method is settled") into a distinct, clearly-headed
      **"Agent operating guidance"** block.
- [x] Add that block to `starter/AGENTS.md` so adopting projects' agents receive
      it (closing today's gap).
- [x] Update the `starter/AGENTS.md` "How we work" pointer to also point newcomers
      at `docs/guide.md`.

### Regenerate this repo's derived rendering
- [x] Regenerate this repo's `AGENTS.md` method body from the canonical spec by
      applying the enumerated deltas (root paths, construction-ADR links, no
      citation, entry-point framing). Add a **header sync note** marking it
      *derived — regenerate from `starter/docs/working-method.md`, do not patch
      alone*.
- [x] Keep this repo's "Agent operating guidance" block in `AGENTS.md` aligned
      with the starter's block (same rules, this-repo framing).
- [x] Regenerate this repo's **`guide.md`** (root) from the canonical
      `starter/docs/guide.md`, applying the path delta (root families, no
      `docs/` prefix). Mark it *derived — do not patch alone*.

### Slim the README to a human landing page
- [x] Reduce `README.md` to a thin, human-first landing page: one line on what
      decision-trail is; a short "**How this repo is organized**" note
      (`ideas/` · `decisions/` (ADRs) · `plans/` · `overview.md`, and that the
      method documents its own construction); and pointers — **newcomers →
      `guide.md`**, **agents → `AGENTS.md`**. Drop the duplicated
      contract/lifecycle prose so README is no longer a place the method text can
      drift.

### Close-out
- [x] Update layout/prose references that now mention the new files
      (`overview.md` prose, `starter/docs/overview.md` prose,
      `.github/copilot-instructions.md` if affected) — not the artifact rows.
- [x] Add a `CHANGELOG.md` entry; this is an adopter-visible structural change
      (new `docs/guide.md`, restructured `working-method.md`, agent block in
      `AGENTS.md`) → choose the version bump and cut the semver tag.
- [x] Regenerate `overview.md` and re-stamp the date; move this plan
      `draft → active → done`.

## Resolved (was open question)

- **README vs. user guide.** README is the human's first landing point and is
  irrelevant to agents → keep it **small and simple**: a few words on how the
  documentation is structured in this repo, plus a pointer to the human Guide.
  This repo therefore **does host its own `guide.md`** (root), a derived
  rendering of the canonical `starter/docs/guide.md`. Reading paths: human →
  README → `guide.md` → spec/ADRs; agent → `AGENTS.md`.
