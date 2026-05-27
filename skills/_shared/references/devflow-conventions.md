# DevFlow Conventions

Shared conventions for the Markdown-first DevFlow skill pack.

## Artifact Model

Use task artifacts under the target project:

```text
.workspaces/specs/{ID}-{slug}/
  spec.md
  plan.md
  task_log.md
  qa_report.md
```

## Hard Rules

- Use Markdown artifacts only.
- Do not create JSON artifacts.
- Do not use or require a dashboard.
- Do not assume a DevFlow CLI exists.
- Do not duplicate the same content across artifacts unless the receiving workflow needs a short summary.
- Keep source edits out of intake and planning.
- Append progress to `task_log.md`.
- Keep the latest log entry near the top of `task_log.md`.

## Status Flow

Use these plain-text states in `task_log.md`:

- `Ready For Planning`
- `Planning Pending Approval`
- `Approved For Build`
- `Build In Progress`
- `Ready For Verify`
- `Verify Failed`
- `Verified`
- `Blocked`

## Approval Gate

Before build work, `plan.md` must contain:

```markdown
## Approval
Status: Approved
Approved by: {name}
Approved at: {date/time}
```

If approval is missing or pending, stop before editing source.

## Evidence Gate

Before reporting verification as passed, gather real evidence:

- Command output from tests, lint, typecheck, build, or targeted checks.
- Manual verification steps with observed result when no command fits.
- Clear note when a planned verification could not run.

If evidence is missing, set verification verdict to `Fail` or `Blocked`, not `Pass`.

## Test Decisions

Use one value per subtask:

- `Required`
- `Manual/Command Only`
- `Not Required`

Default to `Required` for bug fixes, business logic, auth, permissions, persistence, parsers, API contracts, security, concurrency, and meaningful user-visible behavior.

## Next Command Pattern

- After intake: `/31-Plan {ID}`
- After approved planning: `/32-Code {ID}`
- After build: `/33-Verify {ID}`
- After failed verification: `/32-Code {ID}`

