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

| Skill | Phase | Stage | Status | Purpose |
| --- | --- | --- | --- | --- |
| `devflow-feature` | 3 | Feature discovery | Ready | Turn a feature idea into `feature_brief.md` through focused interaction. |
| `devflow-task` | 1 | Task intake | Ready | Create a task workspace with `spec.md` and `task_log.md`. |
| `devflow-plan` | 1 | Planning | Ready | Create `plan.md` with phases, subtasks, test decisions, and approval gate. |
| `devflow-build` | 1 | Build | Ready | Implement an approved plan one subtask at a time. |
| `devflow-verify` | 1 | Verification | Ready | Produce `qa_report.md` with evidence and pass/fail verdict. |
| `devflow-test` | 3 | Testing | Ready | Create or run focused test strategy and `test_report.md`. |
| `devflow-debug` | 3 | Debugging | Ready | Create `debug_report.md` for failures and root-cause investigation. |
| `devflow-review` | 3 | Review | Ready | Create `review_report.md` for plans, code, PRs, or tasks. |
| `devflow-commit` | 3 | Commit prep | Ready | Create `commit_summary.md` and suggest a commit message. |
| `devflow-frontend` | 4 | Frontend specialist | Ready | Guide UI, browser, accessibility, and frontend implementation choices. |
| `devflow-backend` | 4 | Backend specialist | Ready | Guide API, service, auth, and backend implementation choices. |
| `devflow-database` | 4 | Database specialist | Ready | Guide schema, migration, index, and data-integrity choices. |
| `devflow-security` | 4 | Security specialist | Ready | Guide auth, permissions, token, validation, and abuse-risk choices. |
| `devflow-prd` | 5 | Product requirements | Ready | Create `prd.md` for larger initiatives. |
| `devflow-research` | 5 | Research | Ready | Create `research.md` for codebase or external research. |
| `devflow-wiki` | 5 | Knowledge capture | Ready | Create `wiki_note.md` for durable project knowledge. |
| `devflow-changelog` | 5 | Changelog | Ready | Create `changelog_entry.md` after verified work. |
| `devflow-insight` | 5 | Insight extraction | Ready | Create `insight.md` from completed or failed work. |

Dry-run coverage so far:

- `devflow-feature`: added as the lightweight discovery step before task intake.
- `devflow-task`: created Markdown task artifacts.
- `devflow-plan`: created `plan.md` with `Approval: Pending`.
- `devflow-build`: stopped correctly when approval was pending.
- `devflow-build`: started approved build path and created expected failing tests for the first subtask.
- `devflow-verify`: not fully exercised after a completed build yet.
- Phase 3-5 skills are scaffolded and ready for first dry-run.

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
devflow-test   -> focused test strategy/report
devflow-debug  -> root-cause report
devflow-review -> review report
devflow-commit -> commit summary
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
  devflow-test/
  devflow-debug/
  devflow-review/
  devflow-commit/
  devflow-frontend/
  devflow-backend/
  devflow-database/
  devflow-security/
  devflow-prd/
  devflow-research/
  devflow-wiki/
  devflow-changelog/
  devflow-insight/
```

## Next Work

Recommended next steps:

1. Complete an approved build path through implementation.
2. Dry-run `devflow-verify` after a completed build.
3. Dry-run Phase 3-5 skills on one overall example.

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
