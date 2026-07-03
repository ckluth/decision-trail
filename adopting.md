# Adopting decision-trail in your own repo

This is the **on-ramp**. It is the single place that tells you how to start using
decision-trail — and how to keep it up to date — in *your* project. It covers three
scenarios:

1. [**Fresh repo**](#1-fresh-repo) — start a new repo directly with the method.
2. [**Inject into an existing repo**](#2-inject-into-an-existing-repo) — add the
   method to a repo that already has code and history.
3. [**Update**](#3-update-xy--xyn) — move an adopting repo from one version of
   decision-trail to a newer one.

> This document lives in the **decision-trail standard repo**
> (https://github.com/ckluth/decision-trail), not in your repo. Your repo carries a
> `Based on decision-trail vX.Y` citation that points back here; come back to this
> page whenever you need to (re)adopt or upgrade.

## Preconditions

You need only two things:

1. **A git repo** — local or hosted, it makes no difference. decision-trail is plain
   markdown under version control.
2. **An agentic setup** — you work with an agent and your preferred harness. Every
   agent knows how to handle an `AGENTS.md`, which is the method's entry point, so
   there is no harness-specific wiring to do. You can also follow every step below
   by hand.

Everything below is **plain do-guidance**: steps you (or your agent) follow. No tool
is required — the migration steps in particular are written so your agent can
execute them directly.

---

## 1. Fresh repo

Goal: a near-empty repo becomes a decision-trail repo in one move.

1. **Copy the contents of [`starter/`](starter/) into your repo root.** You get:
   - `AGENTS.md` — the method entry point (the "How we work" + "Agent operating
     guidance" blocks);
   - `docs/working-method.md` (the terse spec) and `docs/guide.md` (the narrative
     intro);
   - empty `docs/ideas/`, `docs/decisions/`, `docs/plans/` families,
     `docs/overview.md`, `docs/travel-diary.md`, and `docs/intermediate-artifacts/`;
   - a seed decision `docs/decisions/0001-adopt-decision-trail.md`.
2. **Fill in the placeholders:**
   - In `AGENTS.md`, replace the `# <project name>` heading with your project's name
     and a one-line description.
   - In `docs/decisions/0001-adopt-decision-trail.md`, set the `Date:` and replace
     `vX.Y` with the version you copied (see the citation in
     `AGENTS.md` / `docs/working-method.md`).
3. **Commit.** Your repo now owns its artifacts and its own ADR log starting at
   `0001`. It never inherits the decision-trail standard repo's construction ADRs.

That's it. Capture your first idea in `docs/ideas/`, and work the lifecycle from
there (see `docs/guide.md`).

---

## 2. Inject into an existing repo

Goal: drop the method into a repo that already has content, **without disturbing
anything that is already there**.

1. **Copy `starter/docs/` into your repo's `docs/`.** This adds `working-method.md`,
   `guide.md`, the three empty families, `overview.md`, `travel-diary.md`, and
   `intermediate-artifacts/`. It touches none of your existing files. (If you keep
   docs somewhere other than `docs/`, adjust the paths consistently — the method is
   about the artifacts, not the exact folder name.)
2. **Wire up `AGENTS.md`:**
   - If your repo has **no** `AGENTS.md`, create it from `starter/AGENTS.md`
     (fill in the project name/description placeholder).
   - If your repo **already has** an `AGENTS.md`, keep it and **append** the two
     blocks below verbatim — the `## How we work` pointer block and the
     `## Agent operating guidance` block from `starter/AGENTS.md`. Do not hand-merge
     the method body; it lives in `docs/working-method.md`, and `AGENTS.md` only
     points at it.

   The pointer block to append looks like this (adjust the version):

   ```markdown
   ## How we work

   This project follows **decision-trail** — a generic method for carrying a thought
   through its whole life (idea → proposal → decision → plan → execution) in plain
   markdown. New here? Start with the guide in [`docs/guide.md`](docs/guide.md). The
   terse reference is [`docs/working-method.md`](docs/working-method.md); decision
   records live in [`docs/decisions/`](docs/decisions/), starting with
   [`0001-adopt-decision-trail.md`](docs/decisions/0001-adopt-decision-trail.md).

   Based on decision-trail vX.Y — https://github.com/ckluth/decision-trail
   ```
3. **Seed the adoption decision.** Keep `docs/decisions/0001-adopt-decision-trail.md`,
   set its `Date:`, and record the version you copied. Your pre-existing history and
   any prior decisions coexist untouched: the decision-trail ADR log starts **fresh
   at 0001** and never inherits the standard repo's construction ADRs. (If your repo
   already uses `0001` for something else in the same folder, put decision-trail's
   ADRs in `docs/decisions/` so the sequences don't collide.)
4. **Commit.** From here it is identical to a fresh repo.

---

## 3. Update `X.Y → X.Y+n`

Goal: pull a newer version of decision-trail into an already-adopting repo cheaply
and safely. In the best case it is a no-op; otherwise it is a small, explicit
migration.

1. **Find your current version.** Read the `Based on decision-trail vX.Y` citation
   in your `AGENTS.md` (and `docs/working-method.md`). That is the anchor.
2. **Replace the copied method text** with the target version's copies:
   - overwrite `docs/working-method.md` with the target's
     `starter/docs/working-method.md`;
   - overwrite `docs/guide.md` with the target's `starter/docs/guide.md`;
   - bump the `Based on decision-trail vX.Y` citation to the new version (in both
     `docs/working-method.md` and the `## How we work` block of `AGENTS.md`).

   These are self-contained files, so this is a clean, file-level diff. Your own
   ideas, decisions, and plans are **never** overwritten.
3. **Apply the release migrations.** In this standard repo's
   [`CHANGELOG.md`](CHANGELOG.md), each release carries an **`Adopter migration:`**
   note. Read the notes for every version **between your old version and the target**
   and apply them **in order**. Each is written as steps an agent can execute — for
   example: *"backfill any missing `Date:` header on ideas and plans, then regenerate
   `docs/overview.md`."* When a release's note says **"none"**, there is nothing to
   do for that version.
4. **Record the bump.** Add a short ADR in your own `docs/decisions/` noting that you
   moved to the new version (the method text is copied, not referenced, so the bump
   is a decision worth recording).
5. **Commit.**

---

## Why there's no adoption tool

There isn't a script to run, and that's deliberate. Every step above is either a
plain copy, a small edit, or — for the update migrations — a task written so your
**agent** can carry it out directly (backfilling headers, regenerating
`overview.md`, adding back-links). Since an agentic setup is a precondition, the
agent already *is* the tool; a static script would only duplicate trivial copying
and couldn't know about future releases' migrations anyway.

> A future release may offer this repo as a GitHub *template* for a one-click
> "Use this template" start (recorded as a deferred option in ADR-0008). That is a
> platform convenience, not method tooling.
