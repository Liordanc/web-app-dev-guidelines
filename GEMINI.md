# Premium UI Quality Standards

This repository enforces strict validation gates for web application development. 

**No task may be reported as complete without passing all validation checks.**

## Core mandate

Before claiming any work is finished:
1. **All UI tests pass** — the changed user flow works correctly end-to-end.
2. **All Python/backend tests pass** — APIs, services, and data logic are verified.
3. **Lint and type checks pass** — code quality standards are met.
4. **Visual regression checks pass** — UI appearance is correct (if configured).
5. **Accessibility checks pass** — WCAG 2.1 AA standards are met (if configured).

If any validation fails, the task is **incomplete**. Do not mark it done.

## UI validation (mandatory)

### Playwright E2E tests

For every UI change, run:
```bash
npx playwright test --headed
# or targeted to the changed feature
npx playwright test tests/ui/feature-name.spec.ts --headed
```

Before marking complete, verify:
- [ ] All affected user flows pass in E2E tests.
- [ ] The flow works in all configured browsers (Chrome, Firefox, Safari, Edge).
- [ ] Navigation, forms, and interactions work as intended.
- [ ] Error handling and edge cases are tested.
- [ ] Test output is included in the final response.

If tests fail:
- [ ] Do not claim success.
- [ ] Fix the failing test or the underlying code.
- [ ] Re-run until all pass.

### Component/unit tests (if applicable)

For React/Vue/Angular components:
```bash
npm test -- src/components/ChangedComponent.test.tsx --runInBand
# or all component tests
npm test -- --testPathPattern=components --runInBand
```

Before marking complete, verify:
- [ ] Component renders correctly.
- [ ] Props and state updates behave as expected.
- [ ] User interactions trigger the correct handlers.
- [ ] Edge cases (empty state, loading, error) are covered.

### Visual regression tests (if configured)

If the repo uses visual regression tools (Percy, Chromatic, etc.):
```bash
# Example: Percy
npm run percy:test
# or Chromatic
npm run chromatic -- --only-changed
```

Before marking complete, verify:
- [ ] No unexpected visual changes.
- [ ] Approved visual diffs (if any) are intentional.
- [ ] Report is included in the final response.

### Accessibility validation

If the repo requires WCAG 2.1 AA compliance:
```bash
# Example: axe-playwright
npx playwright test tests/a11y/ --headed
```

Before marking complete, verify:
- [ ] No accessibility violations in the changed UI.
- [ ] Keyboard navigation works.
- [ ] Screen reader labels are correct.
- [ ] Color contrast meets WCAG AA.

## Python/backend validation (mandatory)

### Unit tests

For every Python change, run:
```bash
pytest tests/unit/ -q
# or targeted to the changed module
pytest tests/unit/test_changed_module.py -q
```

Before marking complete, verify:
- [ ] All unit tests pass.
- [ ] New behavior is covered by tests.
- [ ] Edge cases and error paths are tested.
- [ ] Test output is included in the final response.

### Integration tests

If the change affects APIs or service logic:
```bash
pytest tests/integration/ -q
# or specific integration suite
pytest tests/integration/test_api_endpoints.py -q
```

Before marking complete, verify:
- [ ] All integration tests pass.
- [ ] API contracts are validated.
- [ ] Database or external service calls work correctly.

### Type checking

If the repo uses type hints (mypy, pyright, etc.):
```bash
mypy . --strict
# or configured type checker
pyright
```

Before marking complete, verify:
- [ ] No type errors.
- [ ] Type coverage is maintained or improved.

### Lint and formatting

If configured:
```bash
ruff check .
black --check .
# or configured linter
flake8 .
```

Before marking complete, verify:
- [ ] No lint violations.
- [ ] Code is properly formatted.

## Web app build validation

### Build success

```bash
npm run build
# or configured build command
```

Before marking complete, verify:
- [ ] Build completes without errors.
- [ ] No console warnings or deprecations introduced.
- [ ] Build output is optimized (check bundle size if applicable).

### Runtime validation

After build, verify the app runs:
```bash
npm start
# or dev server for testing
```

Before marking complete:
- [ ] App starts without errors.
- [ ] No runtime exceptions in the console.
- [ ] Changed features work in the running app.

## Completion checklist

A task is complete **only** when all applicable items are checked:

- [ ] **UI tests pass**: Playwright E2E or component tests run successfully.
- [ ] **UI coverage**: All affected user flows are tested.
- [ ] **Visual validation**: No unexpected regressions (if visual tests configured).
- [ ] **Accessibility**: WCAG 2.1 AA standards met (if required).
- [ ] **Python tests pass**: Unit and integration tests run successfully.
- [ ] **Type checking passes**: No type errors (if mypy/pyright configured).
- [ ] **Lint passes**: Code meets style standards.
- [ ] **Build succeeds**: `npm run build` completes without errors.
- [ ] **Runtime verified**: App runs and changed features work.
- [ ] **Test evidence included**: Final response includes test output and results.

## Failure policy

If **any** validation fails:
- **Do not claim success or "done".**
- Clearly explain what failed and why.
- Either fix the issue immediately and re-run validation, or stop and report the blocker.
- If a fix is not possible in this session, document the exact failure and remaining work.

## Final response requirements

When reporting a task as complete, the response **must** include:

1. **Summary of changes**: What was added, changed, or fixed.
2. **UI validation results**: 
   - Playwright test output (pass/fail).
   - Browsers tested.
   - Any visual or accessibility findings.
3. **Python/backend validation results**: 
   - Unit test output (pass/fail).
   - Integration test output (pass/fail).
   - Type check results.
4. **Build and runtime validation**:
   - Build output (success/failure).
   - Runtime verification (any errors?).
5. **Lint and formatting**: Pass or fail.
6. **Remaining issues or caveats**: Any known limitations or blockers.

**Never claim a task is complete without this evidence.**

## Examples of incomplete vs. complete

### ❌ Incomplete
"I added the login form. Let me know if it works."
- No tests run.
- No validation evidence.

### ✅ Complete
"I added the login form with validation. Here's what I verified:

**UI Tests:**
```
npx playwright test tests/ui/login.spec.ts
✓ Login form renders
✓ Valid credentials log in the user
✓ Invalid credentials show error
✓ Form validation prevents submission with empty fields
```
All 4 tests passed.

**Python API Tests:**
```
pytest tests/unit/test_auth.py -q
4 passed
```

**Lint:**
```
npm run lint
0 issues found
```

**Build:**
```
npm run build
Successfully compiled.
```

The login flow now works end-to-end in Chrome, Firefox, and Safari."

## Repository-specific commands

If your repo has custom test or validation commands, use those instead of generic ones. Examples:

```bash
# Run all quality checks at once
npm run quality-check
# or
make test

# Run only affected tests
npm run test:changed

# Run specific test suite
npm run test:ui
npm run test:api
```

Prefer repo-specific commands when available.
