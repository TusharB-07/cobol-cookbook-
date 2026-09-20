# Task 008: Multiplication Table 1–10

**Tier:** 🥉 Bronze  
**Issue:** #13

## Task
Write a COBOL program that:
1. Accepts a number `n` from the user
2. Prints the multiplication table for `n` from 1 to 10
3. Format: `n x i = result`

## Acceptance Criteria (Exact Expected Output)

**Input:** `7`

**Output:**
```
7 x 1 = 7
7 x 2 = 14
7 x 3 = 21
7 x 4 = 28
7 x 5 = 35
7 x 6 = 42
7 x 7 = 49
7 x 8 = 56
7 x 9 = 63
7 x 10 = 70
```

**Input:** `12`

**Output:**
```
12 x 1 = 12
12 x 2 = 24
12 x 3 = 36
12 x 4 = 48
12 x 5 = 60
12 x 6 = 72
12 x 7 = 84
12 x 8 = 96
12 x 9 = 108
12 x 10 = 120
```

## Hints
- `PERFORM VARYING WS-I FROM 1 BY 1 UNTIL WS-I > 10`
- `COMPUTE WS-RESULT = WS-N * WS-I`
- Use `DISPLAY` with multiple operands for clean formatting

## Starter Skeleton
```cobol
IDENTIFICATION DIVISION.
PROGRAM-ID. MULTTABL.
*> Author: <your-github-handle>
DATA DIVISION.
WORKING-STORAGE SECTION.
01 WS-N         PIC 9(4).
01 WS-I         PIC 9(2).
01 WS-RESULT    PIC 9(6).
PROCEDURE DIVISION.
    DISPLAY "Enter number: " WITH NO ADVANCING
    ACCEPT WS-N
    PERFORM VARYING WS-I FROM 1 BY 1 UNTIL WS-I > 10
        COMPUTE WS-RESULT = WS-N * WS-I
        DISPLAY WS-N " x " WS-I " = " WS-RESULT
    END-PERFORM
    STOP RUN.
```

## Files to Create
- `multtabl.cbl` — your solution
- `test-input.txt` — one line with test number (e.g., `7`)