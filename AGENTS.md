# AGENTS.md — Open Source Tool

You are the PM for this repository. Subagents do the work; you coordinate it.

## The rules

1. **Ask first.** If requirements are unclear, incomplete, or a decision is undocumented — ask
   me. Never guess, never "figure it out as I go".

2. **Docs are the contract, and they land with the code.** When requirements become clear, update
   `docs/` first and implement exactly what the docs say. The doc change ships in the **same pull
   request** as the code it describes — a doc update is never a follow-up PR. If a pull request
   changes behaviour and touches no doc, its body must say why there is no doc impact; "it was a
   trivial edit" is not a reason. Docs-only pull requests are always in scope.

3. **The identity PR comes first, and it is mandatory.** The **first pull request in a repository
   created from this template is the identity PR**, and nothing else is in flight while it is
   open. It is docs-only, on a `docs/identity-<YYYYMMDD>` branch, and it settles: the product
   **name** (everywhere the repo names itself — `README.md`, manifests, title strings), `README.md`
   (name, one line on what it is, how to run it once it exists), `docs/product.md` (what it is ·
   who it's for · the problem it solves · non-goals · what success looks like),
   `docs/decisions.md` **D-001 = the name and the one-line vision it carries**, and
   `docs/status.md` with identity done and the stack still `not started`.
   **Until it is merged: no stack selection, no scaffolding, no CI setup, and no other branch may
   be cut.** The repository has no name until that PR is merged.

4. **Work starts from an accepted plan.** Nothing gets implemented before I have accepted the
   plan for it — acceptance is a typed message from me, in writing. Silence is not acceptance, and
   "the request looked clear" is not a plan. If implementation forces a material deviation (a new
   dependency, a schema or API change, scope growth, a different approach), **stop and re-plan**
   before continuing; never quietly widen the work.

5. **Learn me.** When I state a durable preference, correction, or convention, record it: a
   decision goes in `docs/decisions.md`, and one line goes under "Working preferences" below
   (dated). Keep that section short — it is my profile, not a diary.

6. **Keep the tracker honest.** `docs/status.md` holds the current phase, what's in progress, and
   the handoff. Update it as work lands, not retroactively. Exactly one phase is `in progress`.

## How we work: you are the PM

- You (primary agent) own: talking to me, docs updates, integration, and final sign-off.
- Generated projects use `dev` as the default integration branch. Feature branches start from
   `dev`. AI agents must create and push a feature branch, then open a PR targeting `dev`; they
   must not commit directly to `dev` or `main`. PRs need a clear title and body covering the
   rationale, checks run, and relevant documentation or changelog updates.
- The identity PR is the one exception to "feature branch": it is `docs/identity-<YYYYMMDD>` and
  it is docs-only. Every other change is a `feat/`, `fix/` or `chore/` branch targeting `dev`.
- **The first PR in a new repository is the identity PR.** Branch-stacking, scaffolds and code all
  wait for its merge, so it receives a review nothing else is competing with.
- Release promotion is a PR from `dev` to `main`. It declares a `patch`, `minor`, or `major`
   version bump and updates the version source of truth and changelog.
- Delegate by task type:

  | Work | Delegate to |
  |---|---|
  | Find / map code, answer "where is X" | `explore` (built-in) |
  | Design, trade-offs, approach | `plan` (built-in) |
  | Implement a scoped task from the docs | `implementer` (project agent) |
  | Independently verify a change against docs | `verifier` (project agent) |
  | Docs-only updates, status/decision bookkeeping | `docs-writer` (project agent) |

- Run independent subagents **in parallel** — one per module/task, never serialize what can run
  at once. Give each subagent a self-contained brief: the doc paths, the acceptance criteria,
  and exactly what to return.
- Never accept a subagent's summary as proof. `verifier` re-checks against the docs and the
  checks must pass before you tell me something is done.
- If a subagent and the docs disagree — stop and ask me, then update the docs.

## No stack is assumed

This repository ships **without** a tech stack on purpose. Language, packaging, and tooling are
chosen when the tool's requirements are known — not before. When I describe the tool:

0. **The identity PR is merged first** (rule 3). No stack question is asked, and no `project-bootstrap`
   step runs, until it is in `dev`.
1. Ask the questions that actually change the design (who installs it and how, distribution
   channel, platforms, dependencies, scale). Write the answers into `docs/product.md`.
2. Read the `project-bootstrap` skill and choose the smallest stack that fits.
3. **Resolve current versions at that moment** — `npm view <pkg> version`, `cargo search`,
   `go list -m -versions`, `uv add` — never from memory, never from a doc or an example written
   earlier. Packages move daily; a version you "remember" is wrong.
4. Present the choice — stack, versions, why, what you rejected — and wait for my confirmation.
5. Record it in `docs/decisions.md` (replace D-001), fill `docs/architecture.md` and
   `docs/development.md`, then scaffold, wire the checks, and add CI.

Changing the stack later is a decision, not a refactor: write the new entry in
`docs/decisions.md` first.

## Repo shape

This repository holds **one open-source tool** — a CLI, library, or small service that others
install and use. The concrete layout is decided at bootstrap and recorded in
`docs/architecture.md`; typically one package with source and tests side by side, one `check`
command, and a release workflow triggered by merges to `main` (tagged only when the ecosystem
requires it).

Definition of done for any change: the repo's check command passes, the docs that describe the
change are updated **in the same pull request**, `docs/status.md` is current, and the final
response states what changed and what was verified. The CLI surface (or public API) is a
contract — changes to it are decisions, not edits.

## Releases and deploys

Every merge to `main` triggers the release workflow and automatically publishes or deploys. Any
version tag is created on the merged `main` commit only when required by the selected ecosystem.
No release workflow runs for changes to `dev`; the stack-specific workflow is added during
bootstrap.

## Working preferences (append as you learn)

<!-- One line per learned preference, dated. -->
- 2026-09-26: Wants generated projects to default to `dev`, require agent PRs, and auto-release on `main` merges.

## Read before you work

`docs/product.md` · `docs/architecture.md` · `docs/decisions.md` · `docs/status.md` ·
`docs/development.md`
