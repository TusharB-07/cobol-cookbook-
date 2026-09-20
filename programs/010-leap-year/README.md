# Task 010: Leap Year Checker

**Tier:** 🥉 Bronze  
**Issue:** #15

## Task
Write a COBOL program that:
1. Accepts a year from the user (4-digit integer)
2. Determines if it's a leap year
3. Prints "Leap year" or "Not a leap year"

Rules:
- Divisible by 4 → leap year
- Except: divisible by 100 → not leap year
- Except: divisible by 400 → leap year

Test cases to pass: 1900 (not), 2000 (leap), 2024 (leap), 2100 (not)

## Acceptance Criteria (Exact Expected Output)

**Input:** `1900`

**Output:**
```
Not a leap year
```

**Input:** `2000`

**Output:**
```
Leap year
```

**Input:** `2024`

**Output:**
```
Leap year
```

**Input:** `2100`

**Output:**
```
Not a leap year
```

## Hints
- `FUNCTION MOD(WS-YEAR, 4)`, `FUNCTION MOD(WS-YEAR, 100)`, `FUNCTION MOD(WS-YEAR, 400)`
- `EVALUATE TRUE` works well:
  - WHEN MOD-400 = 0 → leap
  - WHEN MOD-100 = 0 → not leap
  - WHEN MOD-4 = 0 → leap
  - OTHER → not leap

## Starter Skeleton
```cobol
IDENTIFICATION DIVISION.
PROGRAM-ID. LEAPYEAR.
*> Author: <your-github-handle>
DATA DIVISION.
WORKING-STORAGE SECTION.
01 WS-YEAR      PIC 9(4).
01 WS-MOD4      PIC 9.
01 WS-MOD100    PIC 9.
01 WS-MOD400    PIC 9.
PROCEDURE DIVISION.
    DISPLAY "Enter year: " WITH NO ADVANCING
    ACCEPT WS-YEAR
    COMPUTE WS-MOD4 = FUNCTION MOD(WS-YEAR, 4)
    COMPUTE WS-MOD100 = FUNCTION MOD(WS-YEAR, 100)
    COMPUTE WS-MOD400 = FUNCTION MOD(WS-YEAR, 400)
    EVALUATE TRUE
        WHEN WS-MOD400 = 0
            DISPLAY "Leap year"
        WHEN WS-MOD100 = 0
            DISPLAY "Not a leap year"
        WHEN WS-MOD4 = 0
            DISPLAY "Leap year"
        WHEN OTHER
            DISPLAY "Not a leap year"
    END-EVALUATE
    STOP RUN.
```

## Files to Create
- `leapyear.cbl` — your solution
- `test-input.txt` — one line with test year (e.g., `2024`)