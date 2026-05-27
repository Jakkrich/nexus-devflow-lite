---
name: devflow-verify
description: Markdown-first DevFlow verification. Use for devflow-verify, reviewing .workspaces/specs/{ID}-*/ spec.md, plan.md, task_log.md, changed files, and verification evidence, then writing qa_report.md with a Pass or Fail verdict. Does not create JSON artifacts, use dashboards, or require a CLI.
---

# DevFlow Verify

Perform QA review and produce a pass/fail report.

Before working, read:

- `../_shared/references/devflow-conventions.md` when available
- `references/agents/reviewer.md`

## Core Rules

- Use Markdown artifacts only.
- Do not create JSON artifacts.
- Do not use or require a dashboard.
- Do not assume a DevFlow CLI exists.
- Verify with real command output or explicit manual evidence before reporting pass.
- If verification fails or evidence is missing, set verdict to `Fail`.

## Input

```text
devflow-verify {ID}
```

## Process

1. Locate `.workspaces/specs/{ID}-*/`.
2. Read `spec.md`, `plan.md`, and `task_log.md`.
3. Inspect changed files.
4. Run relevant verification:
   - Commands from `plan.md`
   - Project lint, test, typecheck, or build if available
   - Focused manual checks if commands are not available
5. Check acceptance criteria, correctness, readability, architecture fit, security, performance, test decision alignment, and manual verification gaps.
6. Create or update `qa_report.md` from `references/templates/qa_report.template.md`.
7. Set verdict to `Pass` or `Fail`.

## Output

Report:

- Verdict
- Evidence
- Findings
- Residual risk
- Next command:
  - If pass: human approval or commit workflow later
  - If fail: `devflow-build {ID}`
