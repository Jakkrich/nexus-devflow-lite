---
name: devflow-build
description: Markdown-first DevFlow implementation. Use for /32-Code, implementing an approved .workspaces/specs/{ID}-*/plan.md one unchecked subtask at a time, updating plan.md checkboxes and task_log.md, and running planned verification. Requires Approval Status: Approved before editing source. Does not create JSON artifacts, use dashboards, or require a CLI.
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

## Required Approval Gate

Before editing source, read `plan.md`.

Continue only if:

```markdown
## Approval
Status: Approved
Approved by: {name}
Approved at: {date/time}
```

If status is not `Approved`, stop and ask the user to approve `/31-Plan`.

## Input

```text
/32-Code {ID}
```

## Process

1. Locate `.workspaces/specs/{ID}-*/`.
2. Read `spec.md`, `plan.md`, and `task_log.md`.
3. Select the first unchecked subtask in `plan.md`.
4. Implement only that subtask.
5. Follow referenced patterns.
6. If test decision is `Required`, create or update tests before or with the code change.
7. Run the subtask verification.
8. Update the subtask checkbox in `plan.md`.
9. Append an entry to `task_log.md` with action, files changed, verification command, result, and notes.
10. If implementation reveals the plan is wrong, stop and recommend `/31-Plan {ID}`.

## Output

Report:

- Subtasks completed
- Files changed
- Verification commands run
- Any deviations from plan
- Next command: `/33-Verify {ID}`
