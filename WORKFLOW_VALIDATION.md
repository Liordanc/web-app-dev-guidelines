# Premium Quality Standards: Full Integration Testing

This repository enforces strict validation gates for web application development and document-processing workflows.

**No task may be reported as complete without:**
1. Running the entire application workflow with real or realistic test data.
2. Verifying the final output is correct and complete.
3. Validating all required fields, rows, and columns in the produced file.
4. Checking integration between OCR / parsing / transformation / export stages.
5. Running relevant automated tests before final completion.

## Core mandate

Before claiming any work is finished:
- The **entire workflow** must execute successfully.
- The **final output** (Excel, CSV, JSON, database, report, etc.) must be validated.
- All **fields and columns** must be present and filled correctly.
- The **integration** between all components must work.
- If the output is incomplete, inaccurate, or partially filled, the task is **incomplete**.

---

## Example: Receipt Processing & Excel Export

Your project: OCR receipts → Extract data → Generate Excel sheets

### What MUST be tested

#### ❌ NOT ENOUGH:
"I fixed the OCR parsing. The code compiles and unit tests pass."
- No actual receipt was processed.
- No Excel file was generated.
- No validation of output format or fields.

#### ✅ REQUIRED:
"I fixed the OCR parsing. Here's what I verified:

**Step 1: Run OCR on sample receipt**
- Input: `samples/receipt_sample.jpg`
- OCR output included: vendor, date, amount, tax, payment method, category
- Result: ✓ All fields extracted correctly

**Step 2: Extract missing fields**
- Added logic to detect tax amount from receipt image
- Payment method extracted from receipt footer
- Result: ✓ Fields populated correctly

**Step 3: Generate Excel file**
- Command: `python -m app.processor --input samples/receipt_sample.jpg --output output.xlsx`
- Result: ✓ `output.xlsx` created

**Step 4: Validate Excel structure**
- Columns present: `[Vendor, Date, Amount, Tax, Payment Method, Category]`
- Header row: ✓
- Data row values: ✓
- Numeric columns formatted correctly: ✓
- Result: ✓ Excel structure valid

**Step 5: Validate data accuracy**
- Original receipt: Vendor = "Acme Corp", Amount = 42.50
- Excel output: Vendor = "Acme Corp", Amount = 42.50
- Result: ✓ Data matches original

**Step 6: Test edge cases**
- Receipt with missing tax field → Excel tax column marked N/A ✓
- Multi-line vendor name → handled correctly ✓
- Blurry receipt → OCR still extracted values acceptable for workflow ✓

**Unit tests pass:**
```
pytest tests/unit/test_ocr.py -q
pytest tests/unit/test_excel_generator.py -q
✓ All passed
```

**Build and runtime:**
```
python -m compileall .
✓ No errors
```

The output file is valid, all fields present, and the workflow is ready for production."

---

## Full application testing workflow

### Step 1: Setup

Prepare test data that represents real usage:
```bash
# Example: Receipt processing
ls tests/samples/
- receipt_1.jpg      # normal receipt
- receipt_2.jpg      # blurry receipt
- receipt_3.jpg      # missing tax field
- receipt_4.jpg      # foreign text / special characters
```

### Step 2: Run the application with test data

```bash
# Example for a receipt processing pipeline
python -m app.processor \
  --input tests/samples/receipt_1.jpg \
  --output output.xlsx
```

For other projects, adapt to your workflow:
```bash
# Python pipeline
python scripts/process_data.py --input test_data.csv --output result.xlsx

# Web app
npm run generate-report -- --source test_data.json --output report.html

# CLI tool
./bin/mytool process --file input.txt --format excel
```

### Step 3: Validate output format

Check that the output file has the correct structure:

```bash
# Excel validation
python - <<'PY'
import pandas as pd

df = pd.read_excel('output.xlsx')
print('Columns:', df.columns.tolist())
print('Rows:', len(df))
print(df.head())
PY
```

### Step 4: Validate all required fields are present

Create a checklist specific to your project. For receipt processing:
```
- [ ] Vendor name present
- [ ] Date present and correctly formatted
- [ ] Amount present and numeric
- [ ] Tax amount present or marked N/A when missing
- [ ] Payment method extracted
- [ ] Category assigned
- [ ] No empty values in critical columns
```

For your project, define all required columns and all required fields that cannot be blank.

### Step 5: Validate data accuracy

Compare input vs. output:

```bash
python - <<'PY'
import pandas as pd

df = pd.read_excel('output.xlsx')
print(df.iloc[0].to_dict())
PY
```

Manually verify:
- Vendor name matches the receipt
- Amount matches the receipt
- Date matches the receipt
- Tax and payment method are correct if present
- The project-specific expected values are correct

### Step 6: Test edge cases

Run the full workflow with difficult inputs:

```bash
python -m app.processor --input tests/samples/receipt_blurry.jpg --output output_blurry.xlsx
python -m app.processor --input tests/samples/receipt_missing_tax.jpg --output output_no_tax.xlsx
python -m app.processor --input tests/samples/receipt_foreign.jpg --output output_foreign.xlsx
```

Check:
- the app did not crash,
- the output was still produced,
- critical fields are still correct or intentionally marked as missing,
- no silently dropped values.

### Step 7: Run all automated tests

```bash
# Unit tests
pytest tests/unit/ -q

# Integration tests
pytest tests/integration/ -q

# Type checking
mypy . --strict

# Lint
ruff check .

# Build validation
python -m compileall .
```

### Step 8: Compare before and after (if fixing an existing bug)

If fixing a defect, run the workflow before and after:

```bash
# Before fix
python -m app.processor --input tests/samples/receipt_1.jpg --output output_old.xlsx

# After fix
python -m app.processor --input tests/samples/receipt_1.jpg --output output_new.xlsx
```

Then compare outputs and confirm the corrected version is better and consistent with expected results.

---

## Completion checklist for this project type

- [ ] Application runs without errors with test data
- [ ] Output file is generated
- [ ] All required columns/fields exist in the output
- [ ] All required fields are populated
- [ ] Data accuracy verified against input
- [ ] Edge cases tested
- [ ] Unit tests pass
- [ ] Integration tests pass
- [ ] Type checking passes (if applicable)
- [ ] Lint passes
- [ ] Build succeeds
- [ ] Output inspection confirmed manually

---

## Failure scenarios (task is INCOMPLETE)

❌ "I fixed the OCR. The code compiles and tests pass."
- No actual receipt was processed.
- No output file was checked.
- Task is **incomplete**.

❌ "I added the missing tax column. Here's the code change."
- The column may exist in code but not actually be populated.
- No workflow validation was done.
- Task is **incomplete**.

❌ "I improved OCR accuracy from 85% to 92%."
- Metrics sound good, but the actual generated file was not validated.
- No end-to-end output verification performed.
- Task is **incomplete**.

---

## Final response requirements

When reporting a task as complete, the response **must** include:

1. **Summary of changes**
2. **Full workflow validation results**
3. **Output inspection results**
4. **Evidence that all required fields are present and populated**
5. **Automated test results**
6. **Remaining issues or caveats**

### Required format example

```text
Summary:
- Improved OCR parsing for receipt fields and fixed missing tax extraction.

Workflow validation:
- Ran full pipeline on sample receipt: output.xlsx generated successfully.
- Verified columns: Vendor, Date, Amount, Tax, Payment Method, Category.
- Verified values match source receipt.

Field checks:
- Vendor: Acme Corp ✓
- Date: 2025-01-15 ✓
- Amount: 42.50 ✓
- Tax: 3.50 ✓
- Payment Method: Card ✓
- Category: Office Supplies ✓

Tests:
- pytest tests/unit/test_ocr.py -q → passed
- pytest tests/integration/test_receipt_pipeline.py -q → passed

Conclusion:
- Workflow works end-to-end and output is valid.
```

**Never claim a task is complete without this evidence.**

---

## Repository-specific implementation

Adapt this policy to your actual project:

**For Python document-processing projects:**
```bash
python -m app.process --input sample_data.csv --output result.xlsx
# Validate output file structure and values
```

**For web scraping and extraction projects:**
```bash
python scraper.py --output scraped_data.json
# Validate the JSON structure and all expected fields
```

**For OCR/image parsing projects:**
```bash
python -m processor.ocr --image test.png --output extracted.json
# Validate extracted.json contains all required fields
```

**For data pipeline projects:**
```bash
python -m pipeline.main --source input.csv --target output.db
# Validate database schema and row contents
```

Choose commands and validation steps that match your actual application.
