# Decisions

Append-only log of settled decisions. New entries get the next number, a date, and a sentence of
context. If a decision is reversed, add a new entry that supersedes the old one — never edit
history. The agent records decisions here **before** implementing them (see `AGENTS.md`, rule 2).

## D-001: Stack selection — pending

**Date:** —

**Decision:** Not made yet, on purpose. The stack is chosen when the tool's requirements are
known — see the `project-bootstrap` skill.

Replace this entry before scaffolding, and include:

- Language / runtime — with the exact versions resolved **live** at that moment (not from memory,
  not copied from anywhere).
- Distribution: where users install it from (registry, release binaries, container), and how CI
  produces that artifact.
- Test runner, lint/format, build tool, package manager.
- What was considered and rejected, and why (one line each).

The chosen stack is then described in `docs/architecture.md`, and its commands in
`docs/development.md`.

## D-002: Single-agent workflow and requirement review

**Date:** 2026-09-26

**Decision:** The primary agent handles discovery, documentation, design, implementation, and
verification sequentially without spawning subagents, to avoid unnecessary request throttling.
Before implementing, it reviews requirements and user suggestions for ambiguity, conflicts,
technical inaccuracies, and material risks. It explains evidence and asks for confirmation when
the issue affects scope, architecture, or a public contract; minor, low-risk assumptions may be
stated and handled directly.
