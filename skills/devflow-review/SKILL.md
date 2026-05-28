---
name: devflow-review
description: Markdown-first DevFlow review. Use for devflow-review when reviewing a plan, code change, pull request, or completed task before merge. Produces review_report.md with findings, severity, evidence, and recommendations. Does not create JSON artifacts, use dashboards, or require a CLI.
---

# DevFlow Review

Review a plan or change for risks, bugs, and missing verification.

Before working, read `../_shared/references/devflow-conventions.md` when available.

## Process

1. Identify review target: plan, diff, PR, task workspace, or files.
2. Read the relevant artifacts and changed code.
3. Prioritize bugs, regressions, missing tests, security, and data risks.
4. Create or update `review_report.md` from `references/templates/review_report.template.md`.
5. Recommend next step: revise plan, build fixes, verify, or commit.

