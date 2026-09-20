# Task 014: Phone Formatter

**Tier:** 🥈 Silver  
**Issue:** #19

## Task
Write a COBOL program that:
1. Accepts a 10-digit phone number as a continuous string (e.g., `1234567890`)
2. Formats it as `(123) 456-7890`
3. Prints the formatted version

## Acceptance Criteria (Exact Expected Output)

**Input:** `1234567890`

**Output:**
```
Formatted: (123) 456-7890
```

**Input:** `9876543210`

**Output:**
```
Formatted: (987) 654-3210
```

## Hints
- Input as `PIC X(10)`
- Use reference modification: `WS-INPUT(1:3)`, `WS-INPUT(4:3)`, `WS-INPUT(7:4)`
- Build output: `STRING "(" WS-INPUT(1:3) ") " WS-INPUT(4:3) "-" WS-INPUT(7:4) INTO WS-FORMATTED`

## Starter Skeleton
```cobol
IDENTIFICATION DIVISION.
PROGRAM-ID. PHONEFMT.
*> Author: <your-github-handle>
DATA DIVISION.
WORKING-STORAGE SECTION.
01 WS-INPUT      PIC X(10).
01 WS-FORMATTED  PIC X(16).
PROCEDURE DIVISION.
    DISPLAY "Enter 10-digit phone: " WITH NO ADVANCING
    ACCEPT WS-INPUT
    STRING "(" WS-INPUT(1:3) ") " WS-INPUT(4:3) "-" WS-INPUT(7:4)
        INTO WS-FORMATTED
    DISPLAY "Formatted: " WS-FORMATTED
    STOP RUN.
```

## Files to Create
- `phonefmt.cbl` — your solution
- `test-input.txt` — one line with 10-digit number (e.g., `1234567890`)