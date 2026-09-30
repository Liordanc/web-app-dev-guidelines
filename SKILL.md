# Quality Guidelines Generator

Generates professional quality standards documentation (AGENTS.md, GEMINI.md, WORKFLOW_VALIDATION.md) tailored to your specific project requirements.

## Overview

This skill helps teams establish clear, enforceable quality gates for:
- Web application development (React, Next.js, Vue, Angular)
- Python backend services (FastAPI, Django, Flask)
- Document processing and OCR workflows
- Data pipelines and ETL projects
- Full-stack applications

The skill generates customized documentation that prevents agents/developers from claiming tasks are complete without proper validation.

## Quick Start

Ask the skill to generate standards for your project:

```
"Create quality standards for my Python OCR + Excel export project"
"Generate AGENTS.md and GEMINI.md for my React + FastAPI application"
"Write WORKFLOW_VALIDATION.md for my receipt processing pipeline"
"Improve our existing quality guidelines for better UI testing"
```

The skill will:
1. Ask clarifying questions about your project
2. Generate tailored documentation
3. Create files with project-specific validation commands
4. Suggest improvements to existing standards if needed

## What This Skill Does

### Generate Fresh Standards

If your project doesn't have quality guidelines yet, the skill creates:

- **AGENTS.md** — Core validation requirements for all contributors
- **GEMINI.md** — Strict quality standards for web app + Python development
- **WORKFLOW_VALIDATION.md** — End-to-end testing for business processes (OCR, exports, pipelines)

Each file is customized for your tech stack and project type.

### Enhance Existing Standards

If you already have standards files, the skill can:
- Review them for completeness
- Suggest improvements
- Add missing validation gates
- Update with new project requirements
- Ensure consistency across all guidelines

## Example Workflows

### Scenario 1: Receipt Processing + Excel Export

User asks: "Create quality standards for my OCR receipt processor"

Skill response:
1. Asks: What's your tech stack? Python? Node? How do you generate Excel?
2. Asks: What fields must every receipt have? (Vendor, Date, Amount, Tax, etc.)
3. Asks: What edge cases matter? (Blurry images, missing tax, foreign text?)
4. Generates `WORKFLOW_VALIDATION.md` with:
   - Sample commands to run the pipeline
   - Checklist of required fields per output file
   - Edge case test scenarios
   - Before/after validation examples

### Scenario 2: React + FastAPI Web App

User asks: "Generate standards for my full-stack application"

Skill response:
1. Asks: What's your frontend framework? (React, Next.js, Vue?)
2. Asks: What's your Python backend? (FastAPI, Django, Flask?)
3. Asks: Do you have Playwright E2E tests? Visual regression? Accessibility checks?
4. Generates:
   - `AGENTS.md` with general workflow
   - `GEMINI.md` with strict UI + Python validation gates
   - Specific test commands for your stack

### Scenario 3: Data Pipeline

User asks: "Create guidelines for my CSV → database pipeline"

Skill response:
1. Asks: What's the input format? CSV? JSON? API?
2. Asks: What's the output? Database? Warehouse? File?
3. Asks: What data quality checks are critical?
4. Generates `WORKFLOW_VALIDATION.md` with:
   - Input validation steps
   - Transformation verification
   - Output schema validation
   - Sample record inspection

## File Descriptions

### AGENTS.md

Basic quality standards that apply to **all projects**:
- Definition of "task complete"
- When tests must be run
- What validation means
- Failure policies

### GEMINI.md

Strict quality for **web applications and Python services**:
- UI test requirements (Playwright, Jest, etc.)
- Python test requirements (pytest, type checking, lint)
- Build and runtime validation
- Accessibility and visual regression checks

### WORKFLOW_VALIDATION.md

End-to-end testing for **business process automation**:
- Running entire workflows with test data
- Output file validation
- Field and column verification
- Edge case testing
- Before/after comparison for bug fixes

## Features

✅ **Project-aware** — Generates commands specific to your tech stack  
✅ **Role-based** — Different validation gates for different project types  
✅ **Improvement suggestions** — Analyzes existing files and proposes enhancements  
✅ **Edge case discovery** — Helps you think through failure scenarios  
✅ **Reusable templates** — Standard structure with your customizations  
✅ **Easy updates** — Can regenerate or patch files as project evolves  

## How to Use This Skill

### Generate New Standards

1. Navigate to your project root
2. Ask: "Create quality standards for my [project type]"
3. Answer the skill's questions about your tech stack and requirements
4. The skill generates or updates the necessary files
5. Commit the files to your repository

### Review and Improve Existing Standards

1. Ask: "Review my quality standards and suggest improvements"
2. The skill analyzes your current AGENTS.md, GEMINI.md, WORKFLOW_VALIDATION.md
3. Proposes enhancements (missing validation steps, unclear requirements, etc.)
4. Generates updated versions or specific patch suggestions

### Customize for a Specific Project Type

1. Ask: "Create OCR-focused quality standards for my team"
2. Ask: "Generate standards for React Component Library"
3. Ask: "Write guidelines for Python data science project"

The skill tailors the output to your specific domain.

## Example Interactions

### Interaction 1: Fresh Standards

**You:** "I need quality standards for my receipt processing project. It's Python backend, uses OCR, generates Excel files."

**Skill:** "Great! Let me ask a few clarifying questions:

1. What OCR library are you using? (Tesseract, AWS Textract, Google Vision?)
2. What fields must every receipt have in the output Excel? (Vendor, Date, Amount, Tax, Payment Method?)
3. Are there tricky edge cases you worry about? (Blurry images, missing fields, non-English text?)
4. How do you currently validate that the generated Excel is correct?"

**You:** "We use Tesseract. Required fields are: Vendor, Date, Amount, Tax, Payment Method, Category. We're worried about blurry receipts and missing tax fields. Right now we just check if the file was created, but we don't validate the content."

**Skill:** "Perfect. Here's what I'm generating:

1. **WORKFLOW_VALIDATION.md** — Enforcement that:
   - Full pipeline must run with test receipts
   - Output Excel must have all 6 columns
   - Data must match source receipt
   - Blurry and incomplete receipts must be tested
   - Before/after comparison if fixing OCR bugs

2. **AGENTS.md** — Core rule that tasks aren't complete without running the full workflow

3. **Sample test recipes** — Specific pytest + pandas commands for your stack

Files are ready in your repo. Want me to add anything else?"

### Interaction 2: Improve Existing Standards

**You:** "Our GEMINI.md is old. Can you review it and suggest improvements for modern Playwright testing?"

**Skill:** "I'll review your current GEMINI.md...

**Current state:**
- Has basic UI test requirements ✓
- Mentions Playwright but no specific commands ✗
- No accessibility checks ✗
- No before/after test comparison ✗
- No visual regression integration ✗

**Suggestions:**
1. Add specific Playwright commands (`npx playwright test --headed`, etc.)
2. Add WCAG 2.1 AA accessibility validation section
3. Add Percy or Chromatic integration for visual regression
4. Add edge case UI testing (different screen sizes, browsers)
5. Add 'before/after' comparison for bug fixes

Want me to generate an updated version?"

## Parameters and Options

The skill adapts to these project types:

| Project Type | Generates | Key Validation |
|---|---|---|
| Python OCR/Document Processing | WORKFLOW_VALIDATION.md | Output file inspection, field validation |
| React/Next.js + Python | AGENTS.md + GEMINI.md | UI tests (Playwright), Python tests (pytest) |
| Data Pipeline (ETL) | WORKFLOW_VALIDATION.md | Input/output schema, row counts, data quality |
| Python Web Service (FastAPI/Django) | GEMINI.md | API tests, type checking, integration tests |
| Web Scraping/Extraction | WORKFLOW_VALIDATION.md | Output structure, field completeness, edge cases |
| Full-stack App | AGENTS.md + GEMINI.md | UI + backend + build validation |
| Component Library | GEMINI.md + snapshot tests | Component rendering, visual regressions, accessibility |

## Installation

This skill should be placed in your repository at:
```
.agents/skills/quality-guidelines-generator/
```

Or installed globally at:
```
~/.gemini/antigravity/skills/quality-guidelines-generator/
```

## Example Command

```bash
# After installing skill in your project
# Ask your Antigravity agent or Gemini CLI:

"Using the quality-guidelines-generator skill, create standards for my Python + PostgreSQL web API project"
```

## Best Practices

1. **Run the skill early** — Generate standards when starting a new project
2. **Review with your team** — Discuss the generated files with your developers
3. **Customize for your stack** — Answer the skill's questions accurately
4. **Update annually** — As your project evolves, regenerate or update guidelines
5. **Use as onboarding** — New team members read AGENTS.md to understand quality expectations
6. **Link in README** — Reference your quality standards in the main README

## Common Questions

**Q: Can the skill update my existing files?**  
A: Yes. It can review, enhance, or completely regenerate AGENTS.md, GEMINI.md, WORKFLOW_VALIDATION.md based on your feedback.

**Q: What if my project doesn't fit the templates?**  
A: The skill can be extended for custom project types. Describe your workflow and it will generate tailored standards.

**Q: Do I need all three files?**  
A: Start with AGENTS.md (universal). Add GEMINI.md if you have web UI or Python services. Add WORKFLOW_VALIDATION.md if you have business process automation (pipelines, OCR, exports).

**Q: How often should I regenerate?**  
A: When your tech stack changes, when you add new requirements, or when you want to incorporate lessons learned.

## See Also

- [AGENTS.md](./examples/AGENTS.md) — Example basic standards
- [GEMINI.md](./examples/GEMINI.md) — Example strict quality standards
- [WORKFLOW_VALIDATION.md](./examples/WORKFLOW_VALIDATION.md) — Example end-to-end validation
