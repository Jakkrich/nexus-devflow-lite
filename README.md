# Nexus DevFlow Lite

Markdown-first DevFlow workflows packaged as installable agent skills.

This is the lightweight version of Nexus-DevFlow:

- No JSON artifacts
- No dashboard
- No CLI dependency
- No copied full agent library

Install after publishing this repository:

```bash
npx skills add <owner>/nexus-devflow-lite
```

Install one skill:

```bash
npx skills add <owner>/nexus-devflow-lite --skill devflow-ask
```

## Current Status

Usable now:

| Skill | Command | Status | Purpose |
| --- | --- | --- | --- |
| `devflow-ask` | `/30-Task` | Ready | Create a task workspace with `spec.md` and `task_log.md`. |
| `devflow-plan` | `/31-Plan` | Ready | Create `plan.md` with phases, subtasks, test decisions, and approval gate. |
| `devflow-build` | `/32-Code` | Ready with approval gate | Implement an approved plan one subtask at a time. |
| `devflow-verify` | `/33-Verify` | Ready | Produce `qa_report.md` with evidence and pass/fail verdict. |

Dry-run coverage so far:

- `devflow-ask`: created Markdown task artifacts.
- `devflow-plan`: created `plan.md` with `Approval: Pending`.
- `devflow-build`: stopped correctly when approval was pending.
- `devflow-build`: started approved build path and created tests for the first subtask.
- `devflow-verify`: not fully exercised after a completed build yet.

Known refinement:

- TDD flow should distinguish an expected failing test subtask from a failed implementation subtask.

## Artifact Model

Task artifacts live in the target project:

```text
.workspaces/specs/{ID}-{slug}/
  spec.md
  plan.md
  task_log.md
  qa_report.md
```

## Workflow

```text
/30-Task  -> devflow-ask
/31-Plan  -> devflow-plan
/32-Code  -> devflow-build
/33-Verify -> devflow-verify
```

Typical flow:

```text
/30-Task 001 Add authentication lockout
/31-Plan 001
# user reviews plan.md and approves it
/32-Code 001
/33-Verify 001
```

## Rules

- Markdown-first.
- No JSON artifacts.
- No dashboard.
- No CLI dependency.
- No source edits during `devflow-ask` or `devflow-plan`.
- `devflow-build` requires `plan.md` approval status to be `Approved`.
- `devflow-verify` requires real evidence before a pass verdict.

## Layout

```text
skills/
  _shared/
    references/devflow-conventions.md
  devflow-ask/
    SKILL.md
    references/templates/spec.template.md
    references/templates/task_log.template.md
  devflow-plan/
    SKILL.md
    references/agents/planner.md
    references/templates/plan.template.md
  devflow-build/
    SKILL.md
    references/agents/coder.md
  devflow-verify/
    SKILL.md
    references/agents/reviewer.md
    references/templates/qa_report.template.md
```

## Next Work

Recommended next steps:

1. Refine `devflow-build` for TDD expected-failure subtasks.
2. Complete an approved build path through implementation.
3. Dry-run `devflow-verify` after a completed build.
4. Add the next skills only after core flow is stable: `devflow-test`, `devflow-debug`, `devflow-review`, `devflow-commit`.

