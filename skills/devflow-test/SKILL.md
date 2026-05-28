---
name: devflow-test
description: Markdown-first DevFlow test planning and execution. Use for devflow-test when a task needs test strategy, missing test coverage, focused test commands, or a test_report.md. Does not edit source unless the user asks to add or update tests. Does not create JSON artifacts, use dashboards, or require a CLI.
---

# DevFlow Test

Create or execute a focused test strategy for a task.

Before working, read `../_shared/references/devflow-conventions.md` when available.

## Process

1. Locate the relevant task workspace when an ID is provided.
2. Read `spec.md`, `plan.md`, and `task_log.md` when available.
3. Identify required, missing, and existing tests.
4. Run targeted tests when possible.
5. Create or update `test_report.md` from `references/templates/test_report.template.md`.
6. Recommend next step: `devflow-build`, `devflow-verify`, or `devflow-debug`.

