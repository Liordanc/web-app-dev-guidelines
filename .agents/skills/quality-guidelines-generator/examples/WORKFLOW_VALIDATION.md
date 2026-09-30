# Premium Quality Standards: Full Integration Testing

This repository enforces end-to-end validation of business workflows.

**No task may be reported as complete without running the real workflow and validating the final output.**

## Core mandate

Before claiming completion:
- run the entire workflow with realistic input
- generate the final output file or result
- verify the output structure and content
- validate all required fields and columns
- test edge cases and failure scenarios

## Example: Receipt processing and Excel export

For a receipt OCR project, the workflow is:
1. process a sample receipt image
2. extract fields from the receipt
3. generate an Excel output
4. validate the file schema and values
5. test blurry / partial / missing-data examples

A task is incomplete if:
- the code compiles but no real receipt was processed
- the Excel file is generated but columns are missing
- fields are extracted but not validated against the source
- edge cases were not tested

## Required validation steps

### 1. Run the full workflow

```bash
python -m app.processor --input tests/samples/receipt_1.jpg --output output.xlsx
```

### 2. Validate output structure

```bash
python - <<'PY'
import pandas as pd

df = pd.read_excel('output.xlsx')
print(df.columns.tolist())
print(df.head())
PY
```

### 3. Validate all required fields

Required checks include:
- Vendor present
- Date present and correctly formatted
- Amount present and numeric
- Tax present or marked N/A when missing
- Payment method extracted
- Category assigned
- No empty values in critical columns

### 4. Validate data accuracy

Compare the extracted values to the source receipt and confirm they match.

### 5. Test edge cases

Run the workflow against:
- blurry receipt images
- missing tax fields
- multi-line vendor names
- non-English text

### 6. Run automated tests

```bash
pytest tests/unit/ -q
pytest tests/integration/ -q
```

## Failure policy

If the workflow fails, or the final output is incorrect, incomplete, or partially filled:
- do not say the task is complete,
- explain the specific failure,
- fix the issue,
- and re-run the workflow end-to-end.

## Final response requirements

The final response must include:
- summary of the change,
- workflow commands executed,
- output validation result,
- evidence that all required fields are populated correctly,
- remaining caveats or blockers.

Never claim success without evidence from the actual workflow output.
