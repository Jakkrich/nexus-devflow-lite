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
- Mark implementation subtasks complete only after passing verification.
- Mark test-only subtasks complete when the expected failing test proves the planned missing behavior.
- Append a concise entry to `task_log.md`.

## Expected Failing Test Rule

When the selected subtask only adds tests:

- Run the planned verification command.
- Confirm the new test fails for the expected reason.
- Confirm unrelated tests pass or document unrelated failures.
- Mark the subtask complete if the failure proves the planned behavior is missing.
- Add `expected failing test added` near the completed checkbox or in the subtask notes.
- Log the failing test name, expected failure, and next implementation subtask.

Do not use this rule for implementation subtasks. Implementation subtasks require passing verification.

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
