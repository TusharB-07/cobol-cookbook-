# Task 002: Name Banner

**Tier:** 🥉 Bronze  
**Issue:** #7

## Task
Write a COBOL program that:
1. Accepts a name from the user (up to 20 characters)
2. Prints a greeting with a border made of `*` characters
3. The border should be exactly 2 characters longer than the greeting line

## Acceptance Criteria (Exact Expected Output)

**Input:** `Alice`

**Output:**
```
**************
* Hello, Alice! *
**************
```

**Input:** `Bob`

**Output:**
```
************
* Hello, Bob! *
************
```

## Hints
- Use `ACCEPT WS-NAME` to read input
- Calculate length: `FUNCTION LENGTH(WS-NAME)` or `FUNCTION LENGTH-TRIM(WS-NAME)`
- Build the greeting in a variable: `STRING "Hello, " WS-NAME "!" DELIMITED BY SIZE INTO WS-GREETING`
- Border length = `FUNCTION LENGTH(WS-GREETING) + 4` (for `* ` and ` *`)
- Use `PERFORM` to print the border line, or `DISPLAY` with `FUNCTION REPEAT`

## Starter Skeleton
```cobol
IDENTIFICATION DIVISION.
PROGRAM-ID. NAMEBANNER.
*> Author: <your-github-handle>
DATA DIVISION.
WORKING-STORAGE SECTION.
01 WS-NAME      PIC X(20).
01 WS-GREETING  PIC X(40).
01 WS-BORDER    PIC X(50).
01 WS-LEN       PIC 9(2).
PROCEDURE DIVISION.
    DISPLAY "Enter your name: " WITH NO ADVANCING
    ACCEPT WS-NAME
    *> Build greeting and border here
    STOP RUN.
```

## Files to Create
- `namebanner.cbl` — your solution
- `test-input.txt` — one line with a test name (e.g., `Alice`)