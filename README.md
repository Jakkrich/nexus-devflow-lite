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

## Skill Catalog

All skills are usable now.

| Skill | Phase | What it does | Use case |
| --- | --- | --- | --- |
| `devflow-feature` | 3 | Turns a feature idea into a focused `feature_brief.md`. | "I want team invites, but the flow and edge cases are not clear yet." |
| `devflow-task` | 1 | Creates a task workspace with `spec.md` and `task_log.md`. | "Turn this agreed feature into a concrete task." |
| `devflow-plan` | 1 | Creates `plan.md` with phases, subtasks, test decisions, and approval gate. | "Plan task 001 before coding." |
| `devflow-build` | 1 | Implements an approved plan one subtask at a time. | "Build the first unchecked subtask after I approve the plan." |
| `devflow-verify` | 1 | Creates `qa_report.md` with evidence and pass/fail verdict. | "Check whether the implementation really satisfies the task." |
| `devflow-test` | 3 | Creates or runs focused test strategy and `test_report.md`. | "What tests are missing for this task?" |
| `devflow-debug` | 3 | Creates `debug_report.md` for failures and root-cause investigation. | "This test fails; find the real cause." |
| `devflow-review` | 3 | Creates `review_report.md` for plans, code, PRs, or tasks. | "Review this change before merge." |
| `devflow-commit` | 3 | Creates `commit_summary.md` and suggests a commit message. | "Summarize verified work for commit." |
| `devflow-frontend` | 4 | Guides UI, browser, accessibility, and frontend implementation choices. | "Review this form flow and responsive behavior." |
| `devflow-backend` | 4 | Guides API, service, auth, and backend implementation choices. | "Design the endpoint and error contract." |
| `devflow-database` | 4 | Guides schema, migration, index, and data-integrity choices. | "Should this feature add a table, index, or migration?" |
| `devflow-security` | 4 | Guides auth, permissions, token, validation, and abuse-risk choices. | "Check invite tokens, rate limits, or permission risks." |
| `devflow-prd` | 5 | Creates `prd.md` for larger product initiatives. | "This is bigger than one feature; write a PRD first." |
| `devflow-research` | 5 | Creates `research.md` for codebase or external research. | "Research existing patterns before planning." |
| `devflow-wiki` | 5 | Creates `wiki_note.md` for durable project knowledge. | "Save this verified convention for future tasks." |
| `devflow-changelog` | 5 | Creates `changelog_entry.md` after verified work. | "Draft a changelog entry from this completed task." |
| `devflow-insight` | 5 | Creates `insight.md` from completed or failed work. | "Extract lessons from this task or bug." |

Dry-run coverage:

- `devflow-feature`: added as the lightweight discovery step before task intake.
- `devflow-task`: created Markdown task artifacts.
- `devflow-plan`: created `plan.md` with `Approval: Pending`.
- `devflow-build`: stopped correctly when approval was pending.
- `devflow-build`: started approved build path and created expected failing tests for the first subtask.
- `devflow-verify`: produced a passing `qa_report.md` after completed build.
- Phase 3-5 skills were exercised in one overall dry-run.

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
