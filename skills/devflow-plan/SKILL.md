---
name: devflow-plan
description: Markdown-first DevFlow implementation planning. Use for /31-Plan, reading .workspaces/specs/{ID}-*/spec.md, exploring relevant codebase context, writing plan.md with phases, subtasks, test decisions, verification commands, and an Approval block set to Pending. Does not edit source code, create JSON artifacts, use dashboards, or require a CLI.
---

# DevFlow Plan

Create a codebase-informed implementation plan. Do not edit source code.

Before working, read:

- `../_shared/references/devflow-conventions.md` when available
- `references/agents/planner.md`

## Core Rules

- Use Markdown artifacts only.
- Do not create JSON artifacts.
- Do not use or require a dashboard.
- Do not assume a DevFlow CLI exists.
- Do not edit source code.
- Set `plan.md` approval to `Pending`.
- Present the plan to the user and request explicit approval before build work.

## Input

```text
/31-Plan {ID}
```

## Process

1. Locate `.workspaces/specs/{ID}-*/`.
2. Read `spec.md`.
3. Explore only relevant codebase files:
   - Similar implementations
   - Entry points
   - Tests
   - Config
   - Commands
4. Create or update `plan.md` from `references/templates/plan.template.md`.
5. Set approval block:

```markdown
## Approval
Status: Pending
Approved by:
Approved at:
```

6. For every subtask, include change, files, patterns, test decision, verification, and expected result.
7. Append a planning entry to `task_log.md` when it exists.
8. Report the plan path and recommend `/32-Code {ID}` after approval.

## Test Decision Values

- `Required`
- `Manual/Command Only`
- `Not Required`

Default to `Required` for bug fixes, business logic, auth, permissions, persistence, parsers, API contracts, security, concurrency, and meaningful user-visible behavior.
