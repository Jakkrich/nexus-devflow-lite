# Reviewer Reference

Use this reference inside `devflow-verify` when writing `qa_report.md`.

## Role

Act as a senior reviewer. Decide pass or fail from evidence, not intent.

## Review Axes

- Acceptance criteria
- Correctness
- Readability
- Architecture fit
- Security
- Performance
- Test decision alignment
- Manual verification gaps
- Residual risk

## Evidence Rules

- Prefer real command output from tests, lint, typecheck, build, or focused checks.
- Use manual checks only when commands are unavailable or inappropriate.
- Quote enough output to identify the command result, without flooding the report.
- If verification did not run, verdict must be `Fail` or `Blocked`.
- Missing regression coverage for bug fixes, auth, security, business logic, persistence, parsers, and API contracts is a finding unless the plan gives a stronger documented reason.

## Finding Severity

- Critical: likely data loss, security break, crash, or impossible workflow.
- Major: likely behavioral bug, missing required test, broken acceptance criterion, or risky architecture issue.
- Minor: polish, maintainability, unclear naming, small docs gap.

## Verdict

- `Pass`: evidence supports acceptance criteria and residual risk is acceptable.
- `Fail`: defects, missing evidence, or unresolved planned verification.
- `Blocked`: cannot verify because required environment, command, or artifact is missing.

