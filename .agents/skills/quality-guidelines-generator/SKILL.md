# Quality Guidelines Generator

Generates and improves project quality standards for AI agents and developers.

## Purpose

This skill creates strong validation gates for projects where code alone is not enough. It is especially valuable for:
- web applications and UI work
- Python backends and APIs
- document processing and OCR pipelines
- Excel/CSV/JSON export workflows
- data extraction and ETL systems

The goal is to prevent false completion claims such as:
- "fixed" without running the workflow
- "done" without validating the final output
- "tests pass" without checking the actual business result

## Core behavior

When invoked, this skill should:
1. Understand the project type and stack
2. Ask the minimum required clarifying questions
3. Generate or update quality rules
4. Tailor the validation requirements to the actual workflow
5. Prefer end-to-end verification over code-only validation

## Required output

This skill should generate or update files such as:
- `AGENTS.md`
- `GEMINI.md`
- `WORKFLOW_VALIDATION.md`

The generated content must enforce that tasks are not considered complete without:
- running the relevant tests
- running the application or workflow itself
- validating the real output product
- checking edge cases and failure scenarios
- reporting evidence of execution and results

## Rules for generated documentation

The generated standards should always include:
- a clear completion gate
- validation commands for the stack used
- a required workflow section
- a failure policy for blocked or broken work
- evidence requirements before claiming success

## Project types supported

### Web app / full-stack
Generate standards for:
- frontend tests
- backend tests
- build validation
- UI flow verification
- accessibility and regression checks

### Python service / API
Generate standards for:
- pytest
- linting
- type checking
- integration tests
- API response validation

### Document processing / OCR / export
Generate standards for:
- running the full workflow on sample files
- validating output file structure
- checking required columns and field presence
- verifying values against the source document
- testing edge cases and partial data

## Example prompts

- "Create AGENTS.md for my React + FastAPI project"
- "Write a strict GEMINI.md for my web app with Playwright and pytest"
- "Create WORKFLOW_VALIDATION.md for my receipt OCR + Excel export pipeline"
- "Review our current quality rules and improve them"
- "Add a completion gate that prevents claiming success without full validation"

## Output style

The generated files must be written in clear English and should use professional, enforceable language.

Use language such as:
- "must"
- "required"
- "not complete unless"
- "do not claim success without"

Avoid vague wording like:
- "should be okay"
- "probably works"
- "looks fine"

## Quality principles

This skill must prefer these principles:
- run the real workflow before claiming completion
- validate the actual output, not only the code path
- verify integration and business correctness
- test edge cases and missing values
- report results with evidence

## Example structure

A generated `AGENTS.md` should contain:
- core rule
- required workflow
- completion gate
- validation commands
- failure policy
- final response requirements

A generated `GEMINI.md` should contain:
- UI validation requirements
- backend validation requirements
- build and runtime checks
- accessibility standards when relevant
- completion checklist

A generated `WORKFLOW_VALIDATION.md` should contain:
- end-to-end execution instructions
- output validation steps
- required field checks
- edge case scenarios
- before/after verification process

## Best practices

- Tailor validation to the actual project and workflow
- Prefer the smallest relevant commands that test the changed area
- Run broader checks when the repo requires them
- Require real evidence before final success claims
- If validation cannot be run, report the block clearly

## Completion policy

This skill should never generate standards that allow a task to be marked complete based only on compilation, syntax check, or code review. The output must require operational verification of the real result.
