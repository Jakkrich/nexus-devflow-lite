# Nexus DevFlow Lite

Markdown-first DevFlow workflows packaged as installable agent skills.

This is the lightweight version of Nexus-DevFlow:

- No JSON artifacts
- No dashboard
- No CLI dependency
- No copied full agent library

Install after publishing this repository:

```bash
npx skills add Jakkrich/nexus-devflow-lite
```

Install one skill:

```bash
npx skills add Jakkrich/nexus-devflow-lite --skill devflow-task
```

## Current Status

Usable now:

| Skill | Stage | Status | Purpose |
| --- | --- | --- | --- |
| `devflow-feature` | Feature discovery | Ready | Turn a feature idea into `feature_brief.md` through focused interaction. |
| `devflow-task` | Task intake | Ready | Create a task workspace with `spec.md` and `task_log.md`. |
| `devflow-plan` | Planning | Ready | Create `plan.md` with phases, subtasks, test decisions, and approval gate. |
| `devflow-build` | Build | Ready with approval and TDD expected-failure handling | Implement an approved plan one subtask at a time. |
| `devflow-verify` | Verification | Ready | Produce `qa_report.md` with evidence and pass/fail verdict. |

Dry-run coverage so far:

- `devflow-feature`: added as the lightweight discovery step before task intake.
- `devflow-task`: created Markdown task artifacts.
- `devflow-plan`: created `plan.md` with `Approval: Pending`.
- `devflow-build`: stopped correctly when approval was pending.
- `devflow-build`: started approved build path and created expected failing tests for the first subtask.
- `devflow-verify`: not fully exercised after a completed build yet.

Known refinement:

- Complete an approved build path through implementation and verification.

## Artifact Model

Task artifacts live in the target project:

```text
.workspaces/specs/{ID}-{slug}/
  spec.md
  plan.md
  task_log.md
  qa_report.md
```

Feature discovery artifacts live in:

```text
.workspaces/features/{slug}/
  feature_brief.md
```

## Workflow

```text
devflow-feature -> feature discovery before task intake
devflow-task   -> task intake
devflow-plan   -> implementation plan
devflow-build  -> approved implementation
devflow-verify -> verification report
```

Typical flow:

```text
devflow-feature Add authentication lockout
devflow-task 001 Add authentication lockout
devflow-plan 001
# user reviews plan.md and approves it
devflow-build 001
devflow-verify 001
```

## Rules

- Markdown-first.
- No JSON artifacts.
- No dashboard.
- No CLI dependency.
- No source edits during `devflow-task` or `devflow-plan`.
- `devflow-build` requires `plan.md` approval status to be `Approved`.
- `devflow-verify` requires real evidence before a pass verdict.

## Layout

```text
skills/
  _shared/
    references/devflow-conventions.md
  devflow-feature/
    SKILL.md
    references/templates/feature_brief.template.md
  devflow-task/
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

1. Dry-run `devflow-feature` on a vague feature idea.
2. Complete an approved build path through implementation.
3. Dry-run `devflow-verify` after a completed build.
4. Add later skills only after core flow is stable: `devflow-test`, `devflow-debug`, `devflow-review`, `devflow-commit`.

## devflow-feature

`devflow-feature` is the discovery skill before `devflow-task`.

Purpose:

- Pull hidden requirements out of the user through short interaction.
- Discuss feasibility, risks, and alternatives before creating a task.
- Turn vague feature ideas into a concise feature brief.
- Recommend whether to proceed to `devflow-task`.

Suggested artifacts:

```text
.workspaces/features/{slug}/
  feature_brief.md
```

Recommended flow:

```text
devflow-feature Add team invite flow
devflow-task 001 Add team invite flow
devflow-plan 001
devflow-build 001
devflow-verify 001
```
