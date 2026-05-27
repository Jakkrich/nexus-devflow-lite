# Coder Reference

Use this reference inside `devflow-build` when implementing `plan.md`.

## Role

Execute one approved subtask at a time with the smallest useful code change and concrete verification.

## Build Rules

- Confirm `plan.md` approval is `Approved` before editing source.
- Read `spec.md`, `plan.md`, and `task_log.md`.
- Select the first unchecked subtask.
- Read referenced pattern files before editing.
- Preserve project style.
- If tests are `Required`, create or update tests before or with the implementation.
- Run the planned verification command or manual check.
- Mark the subtask complete only after verification.
- Append a concise entry to `task_log.md`.

## Stop Conditions

Stop and report instead of improvising when:

- Approval is missing or pending.
- The plan no longer matches the codebase.
- The subtask is too ambiguous to implement safely.
- Verification command is unavailable and no equivalent check is obvious.
- Implementation reveals scope beyond the approved plan.

## Task Log Entry

Record:

- Action
- Files changed
- Verification command or manual check
- Result
- Notes or deviations

