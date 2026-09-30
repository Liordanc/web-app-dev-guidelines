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
4. Run relevant lint, type-check, and UI validation commands if configured for the repo.
5. Confirm the results before stating the task is complete.

## Completion gate

A task is not complete unless all of the following are true:
- the relevant automated tests pass,
- UI validation passes for any app flow affected,
- backend/Python validation passes for any API or service logic changed,
- lint/type-check passes if the repo requires them,
- the changed behavior was verified,
- and the final response includes evidence of what was checked.

If a repo-specific test command exists, use it. Do not skip validation because the task is "small" or "obvious".

## Required validation behavior

When working on code changes:
- add or update tests for behavior changes,
- prefer the smallest relevant test scope,
- run the changed-area tests before broader suites if needed,
- and do not hide failing checks.

## Application-specific rules

For web application / frontend work:
- validate the affected UI flows with end-to-end or component tests,
- check the app still renders and interacts correctly,
- verify the changed user flow with the smallest relevant UI test command,
- and do not report success without evidence from the UI test run.

For Python / backend work:
- run the relevant unit tests for changed modules,
- run the relevant API or integration tests when endpoints or data logic changed,
- verify lint/type-check where configured,
- and do not claim backend correctness without test results.

## Typical validation commands

Use the repo's real commands. Common examples:

```bash
# Python
pytest -q
# or targeted tests
pytest tests/test_api.py -q
pytest tests/test_ui_flow.py -q

# Web frontend / JS
npm test
# or targeted UI tests
npx playwright test tests/ui/login.spec.ts
npx jest src/components/Button.test.tsx --runInBand

# Web app / build validation
npm run build
npm run lint
npm run typecheck

# Python service / FastAPI
pytest -q
python -m compileall .
```

If the project has repo-specific commands, prefer those over generic commands.

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
