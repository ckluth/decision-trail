# <project name>

<!--
If this repo already had an AGENTS.md, keep it and append only the
"## How we work" and "## Agent operating guidance" sections below. Otherwise,
replace this heading with your project's name and a short description of what the
project is.
-->

## How we work

This project follows **decision-trail** — a generic method for carrying a thought
through its whole life (idea → proposal → decision → plan → execution) in plain
markdown. New here? Start with the guide in [`docs/guide.md`](docs/guide.md). The
terse reference is [`docs/working-method.md`](docs/working-method.md); decision
records live in [`docs/decisions/`](docs/decisions/), starting with
[`0001-adopt-decision-trail.md`](docs/decisions/0001-adopt-decision-trail.md).

Based on decision-trail vX.Y — https://github.com/ckluth/decision-trail

## Agent operating guidance

These rules are for an AI agent working in this repo:

- **The method is settled.** Use decision-trail; don't redesign the *method*
  casually. (Your project's own decisions are normal work — captured as ideas,
  ADRs, and plans under `docs/`.)
- **Confirmation guard.** Never rush into writing, editing, or implementing. First
  briefly explain what you intend to do, then wait for explicit approval.
  Discussing and proposing is always fine — acting requires a green light.
- **Keep `docs/overview.md` current.** It is a derived snapshot, regenerated
  wholesale from the artifact headers (never hand-patched) and stamped "as of
  <date>". Regenerate it — and update the stamp — after any work that creates an
  artifact or changes a state, and whenever the user asks. Keeping it current is
  the agent's responsibility, never the user's; a user may flip a state directly
  in an artifact, and the next regeneration reconciles the index.
