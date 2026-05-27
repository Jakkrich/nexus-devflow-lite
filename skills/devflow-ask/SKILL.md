---
name: devflow-ask
description: Markdown-first DevFlow task intake. Use for /30-Task, creating .workspaces/specs/{ID}-{slug}/ task folders, writing spec.md and task_log.md, clarifying scope, acceptance criteria, constraints, and open questions. Does not edit source code, create JSON artifacts, use dashboards, or require a CLI.
---

# DevFlow Ask

Create a task workspace and initial human-readable artifacts.

Before working, read `../_shared/references/devflow-conventions.md` when available.

## Core Rules

- Use Markdown artifacts only.
- Do not create JSON artifacts.
- Do not use or require a dashboard.
- Do not assume a DevFlow CLI exists.
- Do not edit source code.
- Keep task artifacts under `.workspaces/specs/{ID}-{slug}/`.

## Input

```text
/30-Task {ID?} {Title} {Description?}
```

If `{ID}` is missing, inspect `.workspaces/specs/` and choose the next numeric ID.

## Process

1. Clarify intent if the request is vague.
2. Classify workflow type: `feature`, `bugfix`, `refactor`, `docs`, `test`, `investigation`, `migration`, or `simple`.
3. Generate a kebab-case slug from the title.
4. Create `.workspaces/specs/{ID}-{slug}/`.
5. Create `spec.md` from `references/templates/spec.template.md`.
6. Create `task_log.md` from `references/templates/task_log.template.md`.
7. Record known acceptance criteria, constraints, assumptions, and open questions.
8. Report the task path and recommend `/31-Plan {ID}`.

## Output

Report:

- Task ID and path
- Workflow type
- Acceptance criteria
- Open questions
- Next command: `/31-Plan {ID}`
