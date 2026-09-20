# Task 009: Sum of Digits

**Tier:** 🥉 Bronze  
**Issue:** #14

## Task
Write a COBOL program that:
1. Accepts a positive integer from the user (up to 9 digits)
2. Calculates the sum of its digits
3. Prints the sum

## Acceptance Criteria (Exact Expected Output)

**Input:** `472`

**Output:**
```
Sum of digits: 13
```

**Input:** `12345`

**Output:**
```
Sum of digits: 15
```

**Input:** `0`

**Output:**
```
Sum of digits: 0
```

## Hints
- Treat input as string (PIC X), loop through each character
- Convert each char to digit: `NUMVAL(WS-CHAR)` or subtract `'0'`
- Or: use arithmetic — repeatedly `DIVIDE BY 10` and accumulate `REMAINDER`
- String approach is simpler for COBOL beginners

## Starter Skeleton
```cobol
IDENTIFICATION DIVISION.
PROGRAM-ID. SUMDIGIT.
*> Author: <your-github-handle>
DATA DIVISION.
WORKING-STORAGE SECTION.
01 WS-INPUT     PIC X(9).
01 WS-LEN       PIC 9.
01 WS-I         PIC 9.
01 WS-SUM       PIC 9(3) VALUE 0.
01 WS-DIGIT     PIC 9.
PROCEDURE DIVISION.
    DISPLAY "Enter number: " WITH NO ADVANCING
    ACCEPT WS-INPUT
    COMPUTE WS-LEN = FUNCTION LENGTH-TRIM(WS-INPUT)
    PERFORM VARYING WS-I FROM 1 BY 1 UNTIL WS-I > WS-LEN
        MOVE WS-INPUT(WS-I:1) TO WS-DIGIT
        ADD WS-DIGIT TO WS-SUM
    END-PERFORM
    DISPLAY "Sum of digits: " WS-SUM
    STOP RUN.
```

## Files to Create
- `sumdigit.cbl` — your solution
- `test-input.txt` — one line with test number (e.g., `472`)