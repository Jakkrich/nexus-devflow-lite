---
name: devflow-feature
description: Interactive Markdown-first DevFlow feature discovery. Use for devflow-feature when a user has a feature idea but requirements, scope, risks, edge cases, or feasibility are not yet clear. Produces a feature_brief.md and recommends whether to proceed to devflow-task. Does not edit source code, create JSON artifacts, use dashboards, or require a CLI.
---

# DevFlow Feature

Turn a feature idea into a clear, discussable feature brief before task intake.

Before working, read `../_shared/references/devflow-conventions.md` when available.

## Core Rules

- Use Markdown artifacts only.
- Do not create JSON artifacts.
- Do not use or require a dashboard.
- Do not assume a DevFlow CLI exists.
- Do not edit source code.
- Ask short, useful questions when requirements are unclear.
- Prefer 1 question at a time unless the user asks for a full checklist.
- Discuss feasibility and tradeoffs before recommending task creation.

## Input

```text
devflow-feature {Feature idea}
```

## Process

1. Restate the feature idea in one sentence.
2. Identify what is known, unknown, and risky.
3. Ask for missing requirements only when needed.
4. Discuss feasible approaches and tradeoffs.
5. Capture:
   - Problem
   - Target users
   - Goal
   - Scope
   - Non-goals
   - User flow
   - Acceptance criteria draft
   - Edge cases
   - Risks
   - Open questions
6. Create `.workspaces/features/{slug}/feature_brief.md` from `references/templates/feature_brief.template.md` when enough context exists.
7. Recommend whether to proceed to `devflow-task`.

## Output

Report:

- Feature brief path, if created
- Key decisions
- Open questions
- Feasibility recommendation
- Next skill: `devflow-task {ID?} {Title}`

