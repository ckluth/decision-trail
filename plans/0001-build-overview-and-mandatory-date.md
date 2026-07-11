# Plan 0001: Build `overview.md` and the mandatory `Date:` convention

- Status: done
- Date: 2026-06-28
- Implements: [ADR-0011](../decisions/0011-an-always-up-to-date-overview-as-a-derived-status-index.md)

## How

ADR-0011 is the spec. This plan carries it into the repo: create the derived
status index as a dated snapshot, make `Date:` a mandatory header field for
ideas and plans, mirror both into the adopter `starter/`, and record the agent's
regenerate-on-demand duty. Then cut version 1.3.0.

## Tasks

### The overview file
- [x] Create `overview.md` at the repo root: an **"as of YYYY-MM-DD" stamp**
      followed by three tables — Ideas, Decisions, Plans — each row: **Name**
      (relative link), **Created** (from the artifact's `Date:`), **State**
      (current status).
- [x] Generate it by reading the artifact headers (regenerate wholesale, do not
      hand-patch); populate from current artifacts: ideas 0001–0003,
      decisions 0001–0012, plan 0001.

### The mandatory `Date:` convention
- [x] Backfill a `Date:` header into ideas that lack one (0001, 0002).
- [x] Update `AGENTS.md`: state that ideas and plans carry a mandatory `Date:`
      header field (where the lifecycle / cross-link conventions are described).

### Agent duty + layout
- [x] Update `AGENTS.md` "Working in this repo (agent guidance)": `overview.md`
      is regenerated from the artifact headers as a dated snapshot — produced on
      explicit user request at any time, and as part of the agent's definition
      of done after any work that creates an artifact or changes a state. Keeping
      it current is the agent's responsibility, never the user's burden.
- [x] Add `overview.md` to the Layout block in `AGENTS.md`.

### Mirror into the adopter starter
- [x] Add `starter/docs/overview.md` — an "as of …" stamp plus the empty
      three-table skeleton for a fresh project.
- [x] Update `starter/docs/working-method.md`: mandatory `Date:` field, the
      regenerated `overview.md` snapshot, and the agent's regenerate-on-demand
      duty.

### Release
- [x] Add a `## [1.3.0]` entry to `CHANGELOG.md` describing the overview feature
      and the mandatory `Date:` convention (ADR-0011).
