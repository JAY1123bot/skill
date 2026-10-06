---
name: change-control
description: Require explicit user confirmation immediately before modifying files, installing dependencies, changing configuration, or mutating external state; use for tasks where Codex must not act beyond an approved change scope.
---

# Change Control

Use this skill as a two-phase workflow: inspect and propose first, mutate only after a fresh, unambiguous confirmation.

## Before confirmation

- Treat the user's request as a request for analysis and a proposed change, not as permission to execute it.
- Perform only read-only inspection needed to understand the request. Do not use `apply_patch`, file-writing commands, installers, package managers, database writes, API mutations, `git commit`, `git push`, or equivalent actions.
- State the intended changes, exact files or systems in scope, commands/tests to run, and any material side effects.
- Ask for one concise confirmation, such as `确认` or `GO`.

## After confirmation

- Proceed only with the exact scope described immediately beforehand.
- A confirmation authorizes that scope once; it does not authorize newly discovered files, broader refactors, deletions, external publication, or additional installations. Stop and request another confirmation when scope changes.
- Keep destructive actions, external messages, publishing, credential changes, and production changes separately identified even when they are part of the same plan.
- Verify the result and report the files or external state changed, tests run, and any remaining risk.

## Interpretation rules

- Read-only answers, diagnostics, searches, and explanations do not need confirmation.
- Do not infer confirmation from silence, an earlier unrelated approval, a tool approval prompt, or a general instruction such as “handle it.”
- If the user explicitly says not to modify anything, remain in read-only mode even if a later step would normally be useful.
- Higher-priority system, developer, platform, and safety instructions still govern this workflow.
