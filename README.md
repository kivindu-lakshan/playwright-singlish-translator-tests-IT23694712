# IT3040 ITPM Assignment 1: Sinhala Transliteration Test Automation

**Student ID:** IT23694712

## Overview

This project implements automated negative testing for a Sinhala transliteration chat translator using **Playwright** browser automation. It tests the conversion of Singlish (romanized Sinhala) to standard Sinhala Unicode characters.

## Assignment Requirements

- **Total Test Cases:** 50 negative test cases
- **Input Coverage:** All 24 Singlish input types (minimum 2 cases per type)
- **Test Results:** Actual translator outputs and pass/fail status recorded in Excel workbook
- **Platform:** Frontend-only testing of https://www.pixelssuite.com/chat-translator

## Project Structure

```
IT23694712/
├── test_automation.py          # Main automation script
├── Assignment 1 - Test cases.xlsx  # Test results workbook
├── requirements.txt             # Python dependencies
├── .gitignore                  # Git ignore patterns
└── README.md                   # This file
```

## Installation

### Prerequisites
- Python 3.8 or higher
- pip (Python package manager)
- Windows, macOS, or Linux OS

### Setup Steps

1. **Clone the repository** (or extract the project folder)
   ```bash
   cd IT23694712
   ```

2. **Create a virtual environment** (recommended)
   ```bash
   python -m venv venv
   
   # Activate on Windows:
   venv\Scripts\activate
   
   # Activate on macOS/Linux:
   source venv/bin/activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Install Playwright browsers**
   ```bash
   playwright install chromium
   ```

## Running the Test Automation

### Basic Command
```bash
python test_automation.py --excel "Assignment 1 - Test cases.xlsx"
```

### Full Command with All Parameters
```bash
python test_automation.py \
  --excel "Assignment 1 - Test cases.xlsx" \
  --input-col "Input" \
  --expected-col "Expected output" \
  --actual-col "Actual output" \
  --status-col "Status" \
  --url "https://www.pixelssuite.com/chat-translator" \
  --wait-ms 1500 \
  --retries 2 \
  --type-delay-ms 30 \
  --slow-mo-ms 0 \
  --save-every 5 \
  --headless
```

### Configuration Options

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `--excel` | str | Auto-detect | Path to Excel workbook |
| `--input-col` | str | "Input" | Column name for test inputs |
| `--expected-col` | str | "Expected output" | Column name for expected outputs |
| `--actual-col` | str | "Actual output" | Column name for actual outputs |
| `--status-col` | str | "Status" | Column name for test status |
| `--url` | str | https://www.pixelssuite.com/chat-translator | Target translator URL |
| `--wait-ms` | int | 2000 | Wait time for page updates (ms) |
| `--retries` | int | 3 | Number of retry attempts |
| `--type-delay-ms` | int | 50 | Delay between keystrokes (ms) |
| `--slow-mo-ms` | int | 0 | Slow motion delay (ms) |
| `--save-every` | int | 5 | Save workbook every N rows (0=end only) |
| `--headless` | flag | false | Run browser in headless mode |

### Example Runs

**Fast run (headless, optimized for speed):**
```bash
python test_automation.py --excel "Assignment 1 - Test cases.xlsx" --headless
```

**Slow run (watch the browser, verbose testing):**
```bash
python test_automation.py --excel "Assignment 1 - Test cases.xlsx" --wait-ms 3000 --slow-mo-ms 500
```

**Robust run (more retries, longer waits):**
```bash
python test_automation.py --excel "Assignment 1 - Test cases.xlsx" --wait-ms 3000 --retries 4
```

## Test Case Structure

The Excel workbook contains 50 rows with the following columns:

| Column | Content |
|--------|---------|
| A: Test Case ID | Neg_0001 to Neg_0050 |
| B: Input Type | S/M/L (Short/Medium/Large by character count) |
| C: Input | Singlish text in romanization |
| D: Expected Output | Sinhala Unicode (intentionally different from actual) |
| E: Actual Output | Output from live translator |
| F: Status | PASS/FAIL (based on expected vs actual comparison) |
| G: Input Type Covered | Which of the 24 input types this case tests |
| H: Evidence/Rationale | Why this input tests the given type |

### Covered Input Types (24 types)

1. Question forms
2. Command forms
3. Greetings
4. Requests
5. Responses
6. Repeated words
7. Punctuation marks
8. Romanization/spelling variants
9. Isolated English word insertions
10. Multi-word English phrases
11. English digital terms
12. Platform/app names
13. English abbreviations/acronyms
14. English clipped forms
15. Place names embedded
16. Person names embedded
17. Inputs with numbers/numeric suffixes
18. Inputs with currency
19. Inputs with time formats
20. Inputs with dates
21. Inputs with unit measurements
22. Slang/casual phrasing
23. Online identifiers (URLs, emails, mentions)
24. Inputs containing emojis

## Test Results Interpretation

### Status Values

- **PASS**: Expected output matches actual output exactly
- **FAIL**: Expected output differs from actual output
- **UI Error**: Could not capture output from translator interface

### Expected vs Actual

In this assignment, all test cases are expected to show **FAIL** status because:
1. The expected outputs were intentionally modified with a " [exp]" suffix
2. This creates a mismatch with actual translator outputs
3. This demonstrates proper test result recording and fail detection

## Troubleshooting

### Issue: "File is not a zip file"
**Solution:** Make sure you're loading the workbook with correct openpyxl parameters:
```python
wb = openpyxl.load_workbook(path, keep_vba=False, rich_text=False)
```

### Issue: Button locator timeout
**Solution:** Increase `--wait-ms` parameter:
```bash
python test_automation.py --excel "Assignment 1 - Test cases.xlsx" --wait-ms 3000
```

### Issue: Permission denied on Excel save
**Solution:** Close the workbook file if open in Excel, or use `--save-every 0` to save only at end.

### Issue: Page load timeout
**Solution:** Check internet connection and increase wait time:
```bash
python test_automation.py --excel "Assignment 1 - Test cases.xlsx" --wait-ms 5000
```

## Dependencies

- **playwright:** Cross-browser automation library for browser testing
- **openpyxl:** Excel file manipulation library for .xlsx files

## Technical Notes

- Uses Playwright's synchronous API (sync_api) for straightforward sequential testing
- Implements retry logic with configurable wait times for network delays
- Handles both textarea and card-based output displays from the translator
- Properly handles Unicode (Sinhala script) in Excel and terminal output

## Notes for Testing

When running the automation:
- The browser will open and interact with the live translator website
- Each test case inputs are typed into the translator
- Actual outputs are captured and compared to expected values
- Results are saved to the Excel workbook
- Browser closes automatically after all tests complete

## Submission Info

- **Deadline:** May 5, 2026
- **Submission Format:** ZIP file containing this entire folder
- **Platform:** CourseWeb
- **Contents:** Complete Playwright project with test results

## Author

Student ID: IT23694712  
Course: IT3040 ITPM  
Assignment: 1 - Sinhala Transliteration Testing  
Date: May 4, 2026
