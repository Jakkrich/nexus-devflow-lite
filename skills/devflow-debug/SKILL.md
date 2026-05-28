---
name: devflow-debug
description: Markdown-first DevFlow debugging and root-cause investigation. Use for devflow-debug when build, tests, verification, or runtime behavior fails and the root cause is not known. Produces debug_report.md with reproduction, fail path, hypotheses, evidence, and next action. Does not create JSON artifacts, use dashboards, or require a CLI.
---

# DevFlow Debug

Find the real cause of a failure before changing code.

Before working, read `../_shared/references/devflow-conventions.md` when available.

## Process

1. Reproduce the failure or state why it cannot be reproduced.
2. Trace the fail path from input to failure.
3. List hypotheses and what would disprove them.
4. Run the smallest useful experiment.
5. Create or update `debug_report.md` from `references/templates/debug_report.template.md`.
6. Recommend next step: `devflow-build`, `devflow-plan`, or `devflow-verify`.

