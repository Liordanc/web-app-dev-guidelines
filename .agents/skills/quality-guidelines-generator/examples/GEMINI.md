# Premium UI Quality Standards

This repository enforces strict validation gates for web application development.

**No task may be reported as complete without passing all validation checks.**

## Core mandate

Before claiming any work is finished:
1. All UI tests pass.
2. All Python/backend tests pass.
3. Lint and type checks pass if configured.
4. Build and runtime validation pass.
5. Accessibility and regression checks pass when required.

If any validation fails, the task is incomplete.

## UI validation (mandatory)

For every UI change, run the relevant Playwright or component tests:

```bash
npx playwright test --headed
# or a targeted suite
npx playwright test tests/ui/feature-name.spec.ts --headed
```

Before marking complete, verify:
- affected user flows pass
- browser compatibility is acceptable
- forms and error states work correctly
- no UX regression is introduced

## Python/backend validation (mandatory)

For every Python change, run relevant tests:

```bash
pytest tests/unit/ -q
pytest tests/integration/ -q
```

Also run:
```bash
mypy . --strict
ruff check .
```

## Build and runtime validation

```bash
npm run build
npm start
```

Verify the app starts, runs, and the changed flow works in the running application.

## Failure policy

If any validation fails:
- do not claim success,
- explain the failure,
- fix the issue or report the blocker,
- and re-run the validation.

## Final response requirements

The final response must include:
- summary of changes,
- commands run,
- pass/fail result,
- remaining caveats or blockers.
