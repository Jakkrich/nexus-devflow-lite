---
name: devflow-build
description: Markdown-first DevFlow implementation. Use for devflow-build, implementing an approved .workspaces/specs/{ID}-*/plan.md one unchecked subtask at a time, updating plan.md checkboxes and task_log.md, and running planned verification. Requires Approval Status: Approved before editing source. Does not create JSON artifacts, use dashboards, or require a CLI.
---

# DevFlow Build

Implement one approved planned subtask at a time.

Before working, read:

- `../_shared/references/devflow-conventions.md` when available
- `references/agents/coder.md`

## Core Rules

- Use Markdown artifacts only.
- Do not create JSON artifacts.
- Do not use or require a dashboard.
- Do not assume a DevFlow CLI exists.
- Read `spec.md`, `plan.md`, and `task_log.md` before editing.
- Implement only one unchecked subtask at a time unless the user clearly asks to continue.
- Run the subtask verification before marking it complete.
- For test-only subtasks, an expected failing test can complete the subtask when the failure exactly matches missing planned behavior.
- For implementation subtasks, verification must pass before marking the subtask complete.

## Required Approval Gate

Before editing source, read `plan.md`.

Continue only if:

```markdown
## Approval
Status: Approved
Approved by: {name}
Approved at: {date/time}
```

If status is not `Approved`, stop and ask the user to approve the plan from `devflow-plan`.

## Input

```text
devflow-build {ID}
```

## Process

1. Locate `.workspaces/specs/{ID}-*/`.
2. Read `spec.md`, `plan.md`, and `task_log.md`.
3. Select the first unchecked subtask in `plan.md`.
4. Implement only that subtask.
5. Follow referenced patterns.
6. If test decision is `Required`, create or update tests before or with the code change.
7. Run the subtask verification.
8. Decide completion:
   - Test-only subtask: may complete on an expected failing test that proves missing planned behavior.
   - Implementation subtask: complete only when verification passes.
   - Unexpected failure: leave unchecked and stop.
9. Update the subtask checkbox in `plan.md` only when the completion rule is satisfied.
10. Append an entry to `task_log.md` with action, files changed, verification command, result, and notes.
11. If implementation reveals the plan is wrong, stop and recommend `devflow-plan {ID}`.

## Output

Report:

- Subtasks completed
- Files changed
- Verification commands run
- Any deviations from plan
- Next skill: `devflow-verify {ID}`
