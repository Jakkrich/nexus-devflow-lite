# Planner Reference

Use this reference inside `devflow-plan` when turning `spec.md` into `plan.md`.

## Role

Create a small, codebase-informed implementation plan that another agent can execute without guessing.

## Planning Rules

- Read the task `spec.md` first.
- Inspect only codebase files that influence the plan.
- Prefer existing project patterns over new abstractions.
- Keep phases ordered by dependency.
- Keep subtasks independently verifiable.
- Do not edit source code.
- Do not create JSON artifacts.
- Set approval to `Pending`.

## Each Subtask Must Include

- Change: concrete implementation action.
- Files: paths to modify or create.
- Patterns: existing files or conventions to follow.
- Test decision: `Required`, `Manual/Command Only`, or `Not Required`.
- Verification: exact command or manual check.
- Expected: passing evidence.

## Risk Defaults

Default test decision to `Required` for:

- Bug fixes
- Business logic
- Auth or permission logic
- Persistence
- Parsers
- API contracts
- Security-sensitive behavior
- Concurrency
- User-visible behavior with meaningful branching

Use `Not Required` only when the change is docs-only, metadata-only, or has no behavior surface. Still provide a verification path.

