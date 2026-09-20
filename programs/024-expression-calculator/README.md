# Task 024: Expression Calculator

**Tier:** 🥇 Gold  
**Issue:** #29

## Task
Write a COBOL program that:
1. Accepts a simple arithmetic expression from stdin: `num1 op num2`
   - Supported ops: `+`, `-`, `*`, `/`
   - Example: `12 + 4`, `100 / 25`, `7 * 6`, `50 - 30`
2. Parses the three parts
3. Computes and prints the result

## Acceptance Criteria (Exact Expected Output)

**Input:** `12 + 4`

**Output:**
```
12 + 4 = 16
```

**Input:** `100 / 25`

**Output:**
```
100 / 25 = 4
```

**Input:** `7 * 6`

**Output:**
```
7 * 6 = 42
```

**Input:** `50 - 30`

**Output:**
```
50 - 30 = 20
```

**Input:** `10 / 3`

**Output:**
```
10 / 3 = 3.33
```

## Hints
- Read entire line: `ACCEPT WS-LINE`
- Parse with `UNSTRING WS-LINE DELIMITED BY " " INTO WS-N1 WS-OP WS-N2`
- `EVALUATE WS-OP` for operation selection
- Division: use `PIC 9(5)V99` for result, `COMPUTE WS-RESULT = WS-N1 / WS-N2`

## Starter Skeleton
```cobol
IDENTIFICATION DIVISION.
PROGRAM-ID. EXPRCALC.
*> Author: <your-github-handle>
DATA DIVISION.
WORKING-STORAGE SECTION.
01 WS-LINE      PIC X(20).
01 WS-N1        PIC 9(5)V99.
01 WS-OP        PIC X.
01 WS-N2        PIC 9(5)V99.
01 WS-RESULT    PIC 9(5)V99.
PROCEDURE DIVISION.
    DISPLAY "Enter expression (e.g., 12 + 4): " WITH NO ADVANCING
    ACCEPT WS-LINE
    UNSTRING WS-LINE DELIMITED BY " "
        INTO WS-N1, WS-OP, WS-N2
    EVALUATE WS-OP
        WHEN "+"
            COMPUTE WS-RESULT = WS-N1 + WS-N2
        WHEN "-"
            COMPUTE WS-RESULT = WS-N1 - WS-N2
        WHEN "*"
            COMPUTE WS-RESULT = WS-N1 * WS-N2
        WHEN "/"
            IF WS-N2 = 0
                DISPLAY "Error: Division by zero"
                STOP RUN
            END-IF
            COMPUTE WS-RESULT = WS-N1 / WS-N2
        WHEN OTHER
            DISPLAY "Error: Invalid operator"
            STOP RUN
    END-EVALUATE
    DISPLAY WS-N1 " " WS-OP " " WS-N2 " = " WS-RESULT
    STOP RUN.
```

## Files to Create
- `exprcalc.cbl` — your solution
- `test-input.txt` — one line with test expression (e.g., `12 + 4`)