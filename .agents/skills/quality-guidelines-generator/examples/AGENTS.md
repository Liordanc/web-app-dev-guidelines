# Agent Instructions

This repository requires explicit validation before any task may be reported as complete.

## Core rule

Do not claim the task is finished, successful, or "done" unless all required validation checks have been run and passed.

If validation cannot be completed, the agent must clearly say:
- what was validated,
- what failed or was blocked,
- what remains to be done,
- and whether the task is incomplete.

## Required workflow

Before reporting completion:
1. Understand the user request and the code paths affected.
2. Make the minimal correct change.
3. Run the relevant tests for the changed behavior.
4. Run relevant lint, type-check, and build validation commands if configured for the repo.
5. Confirm the results before stating the task is complete.

## Completion gate

A task is not complete unless all of the following are true:
- the relevant automated tests pass,
- UI validation passes for any app flow affected,
- backend/Python validation passes for any API or service logic changed,
- lint/type-check passes if the repo requires them,
- the changed behavior was verified,
- and the final response includes evidence of what was checked.

## Required validation behavior

When working on code changes:
- add or update tests for behavior changes,
- prefer the smallest relevant test scope,
- run the changed-area tests before broader suites if needed,
- and do not hide failing checks.

## Failure policy

If any required validation fails:
- do not say "fixed" or "done",
- explain the error clearly,
- and either fix it or stop and report the blocker.

## Final response requirements

When finishing a task, the final response must include:
- a short summary of the change,
- which validation commands were run,
- their result,
- and any remaining caveats or blockers.

Never claim success without test evidence.
