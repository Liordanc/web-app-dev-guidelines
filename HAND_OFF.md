# HAND OFF: Quality Guidelines Framework

## Overview

This document transfers the Quality Guidelines Framework from `web-app-dev-guidelines` repository to your `isitdone` project.

## What was created in `web-app-dev-guidelines`

A comprehensive quality standards framework consisting of:

### Core Files

1. **AGENTS.md** — Basic validation requirements for all contributors
   - Completion gate: tests must pass before claiming done
   - Core rule: validate before declaring success
   - Failure policy: report blockers, don't hide issues

2. **GEMINI.md** — Strict quality standards for web apps and Python services
   - UI validation (Playwright E2E tests)
   - Python backend validation (pytest, type checking, lint)
   - Build and runtime verification
   - Accessibility checks when required

3. **WORKFLOW_VALIDATION.md** — End-to-end validation for business workflows
   - Run entire workflow with test data
   - Validate output file structure and content
   - Check all required fields and columns
   - Test edge cases and partial data scenarios
   - Before/after comparison for bug fixes

4. **SKILL.md** — Definition of quality-guidelines-generator skill
   - Purpose: generate and improve quality standards
   - Core behavior: understand project, generate tailored rules
   - Supported project types: web app, Python service, OCR/document processing, data pipeline

### Skill Structure

Located at: `.agents/skills/quality-guidelines-generator/`

Contains:
- SKILL.md (skill definition)
- examples/ folder with sample AGENTS.md, GEMINI.md, WORKFLOW_VALIDATION.md

## How to use this framework in `isitdone`

### Step 1: Determine your project type

Is `isitdone`:
- A web application with UI and Python backend?
- A document/receipt processing system with OCR and Excel export?
- A data pipeline or ETL workflow?
- Something else?

### Step 2: Copy the appropriate files to `isitdone`

**If web app + Python backend:**
```bash
cp web-app-dev-guidelines/AGENTS.md isitdone/
cp web-app-dev-guidelines/GEMINI.md isitdone/
```

**If OCR/document processing + export:**
```bash
cp web-app-dev-guidelines/AGENTS.md isitdone/
cp web-app-dev-guidelines/WORKFLOW_VALIDATION.md isitdone/
```

**If both:**
```bash
cp web-app-dev-guidelines/AGENTS.md isitdone/
cp web-app-dev-guidelines/GEMINI.md isitdone/
cp web-app-dev-guidelines/WORKFLOW_VALIDATION.md isitdone/
```

### Step 3: Customize for `isitdone` specifics

Edit the copied files to include:
- Your actual test commands (`pytest tests/...`, `npm test`, etc.)
- Your actual build commands (`npm run build`, `python -m build`, etc.)
- Your required fields and columns (for workflow validation)
- Your edge cases and failure scenarios

### Step 4: Commit and use

Commit the files to `isitdone` repository:
```bash
git add AGENTS.md GEMINI.md WORKFLOW_VALIDATION.md
git commit -m "Add quality standards and validation gates"
```

From that point on, every agent/developer must follow these standards before claiming a task is complete.

## Critical questions for `isitdone`

To properly tailor the quality standards, answer:

### Project Type
- [ ] What is `isitdone` about? (What does it do?)
- [ ] Web application with UI? Python backend only? Both?
- [ ] Does it process documents/images (OCR)? Generate files (Excel/CSV/JSON)?

### Tech Stack
- [ ] Frontend framework (React, Vue, Next.js, vanilla JS)?
- [ ] Backend framework (FastAPI, Django, Flask, Node/Express)?
- [ ] Testing libraries (Playwright, Jest, pytest, etc.)?
- [ ] Any special dependencies (Tesseract, pandas, etc.)?

### Workflows and Outputs
- [ ] What's the main business process? (What does a user do?)
- [ ] What are the inputs? (Files, forms, APIs?)
- [ ] What are the outputs? (Excel files, database records, reports?)
- [ ] What fields/columns are required in the output?

### Edge Cases
- [ ] What can go wrong? (Blurry images, missing data, invalid input?)
- [ ] How should the system behave when data is incomplete or invalid?
- [ ] Are there performance requirements?

### Validation
- [ ] How do you currently test that work is "complete"?
- [ ] Are there automated tests? Manual checks?
- [ ] How do you validate the final output?

## Next Steps

1. **Start a new conversation** focused on `isitdone` with this HAND OFF document
2. **Answer the critical questions** above
3. **Receive customized AGENTS.md, GEMINI.md, WORKFLOW_VALIDATION.md** for `isitdone`
4. **Copy these files** into the `isitdone` repository
5. **Commit and enforce** them as your quality standards

## Key Principle to Remember

The framework enforces this core rule:

> **No task is complete without:**
> - Running the relevant tests
> - Running the actual application or workflow
> - Validating the real output (not just the code)
> - Testing edge cases
> - Reporting evidence before claiming success

This applies to:
- Web app UI changes → must run Playwright tests AND the app itself
- Python API changes → must run pytest AND hit the API AND validate responses
- OCR/document processing → must run the pipeline AND validate the output file
- Data export → must generate the file AND verify all columns and values

## Reference

- GitHub: https://github.com/Liordanc/web-app-dev-guidelines
- SKILL.md: Defines the quality-guidelines-generator skill for creating/improving standards
- Examples: Available in `.agents/skills/quality-guidelines-generator/examples/`

---

**Ready to begin the next phase?**

Answer the critical questions above, then we'll generate the perfect AGENTS.md + GEMINI.md + WORKFLOW_VALIDATION.md for `isitdone`.
