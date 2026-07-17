# Plan 0031: Reframe updating.agent.md step 2 as enumerate-and-copy, ship 2.18.2

- Date: 2026-07-17
- Status: done
- Implements: [ADR-0042](../decisions/0042-reframe-update-step-2-as-enumerate-and-copy.md)

Mechanical execution of ADR-0042: reframe `updating.agent.md` step 2 so the re-copy
is expressed as *"enumerate every subfolder detected under the source's
`starter/docs/` and copy each, overwriting — except the project-authored
folders/files"*, so the agent **discovers** subfolders instead of working from a
named example list (which silently dropped `docs/scripts/` at v2.18). Ship it as the
**2.18.2** patch with a **"none"** migration note (pure wording refinement, no
adopter-visible behavioral change). `starter/` stays the single source of truth; no
manifest; ADR-0022's mechanics unchanged (execution-detail amendment only).

## Tasks

- [x] Edit `updating.agent.md` step 2: replace "copy everything … including but not
      limited to …" with *enumerate the subfolders detected under
      `<source>/starter/docs/` and copy each, overwriting*, keeping the unchanged
      preserve-list of project-authored folders/files never overwritten.
- [x] Add a `CHANGELOG.md` `[2.18.2]` entry with a **"none" `Adopter migration:`**
      note explaining it is a pure wording refinement (discover subfolders, not a
      named list) with no adopter-visible behavioral change.
- [x] Bump the three `starter/` provenance citations v2.18.1 → **v2.18.2**
      (`starter/AGENTS.md`, `starter/docs/working-method.md`, `starter/docs/guide.md`).
- [x] Verify the reciprocal `Amended by: ADR-0042` is present on ADR-0022 (added at
      acceptance).
