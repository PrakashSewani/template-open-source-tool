# Status

Persistent project tracker and handoff. The agent updates this as work lands — see `AGENTS.md`,
rule 4. Keep exactly one phase `in progress`.

## Phase tracker

| Phase | Scope | Status |
|---|---|---|
| 0 | Identity: name, `README.md`, `docs/product.md` vision, D-001 — the identity PR (rule 3) | in progress |
| 1 | Requirements + stack selection: choose the stack, record D-001 (stack) | not started |
| 2 | Scaffold: structure, checks, CI, release path — recorded in `docs/architecture.md` / `development.md` | not started |
| 3 | Core behavior: the one workflow the tool exists for, end to end, with tests | not started |
| 4 | Polish: README, `--help`, error messages, docs — the parts users judge first | not started |
| 5 | Release: main-merge release verified; required tag, artifact, or deployment path checked from a clean environment | not started |

## Current handoff

**Phase:** 0 — waiting for the product name and vision (the identity PR).

**Next action:** fill in `docs/product.md` for a concrete project and run `project-bootstrap`; it
will apply the `dev`-default branch model and add the stack-specific release-on-`main` workflow.

---

### Handoff note format (replace the section above when you stop mid-phase)

- **Phase:** <number and name>
- **Done this session:** <what actually landed>
- **Verified:** <what was run, what was observed — not "it works">
- **Blocked by:** <nothing, or the exact question waiting on the human>
- **Next action:** <the single first thing to do next>
