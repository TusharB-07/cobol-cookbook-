# Task 003: Simple Interest Calculator

**Tier:** 🥉 Bronze  
**Issue:** #8

## Task
Write a COBOL program that reads three values from stdin (one per line):
1. Principal amount (e.g., `10000`)
2. Rate of interest per annum (e.g., `5.5` for 5.5%)
3. Time in years (e.g., `2`)

Calculate and print the simple interest and total amount, both formatted to 2 decimal places.

Formula: `SI = (P × R × T) / 100`, `Amount = P + SI`

## Acceptance Criteria (Exact Expected Output)

**Input:**
```
10000
5.5
2
```

**Output:**
```
Simple Interest: 1100.00
Total Amount: 11100.00
```

**Input:**
```
5000
10
3
```

**Output:**
```
Simple Interest: 1500.00
Total Amount: 6500.00
```

## Hints
- Use `PIC 9(7)V99` for currency values (7 digits before decimal, 2 after)
- `ACCEPT` reads as string — use `NUMVAL` or `NUMVAL-C` to convert, or just `ACCEPT` into a numeric field
- `COMPUTE WS-SI = (WS-P * WS-R * WS-T) / 100`
- For 2-decimal display: `DISPLAY "Simple Interest: " WS-SI` with `PIC 9(7).99` or use `EDIT` mask

## Starter Skeleton
```cobol
IDENTIFICATION DIVISION.
PROGRAM-ID. SIMPLEINT.
*> Author: <your-github-handle>
DATA DIVISION.
WORKING-STORAGE SECTION.
01 WS-P         PIC 9(7)V99.
01 WS-R         PIC 9(3)V99.
01 WS-T         PIC 9(2).
01 WS-SI        PIC 9(7)V99.
01 WS-AMT       PIC 9(7)V99.
PROCEDURE DIVISION.
    ACCEPT WS-P
    ACCEPT WS-R
    ACCEPT WS-T
    COMPUTE WS-SI = (WS-P * WS-R * WS-T) / 100
    COMPUTE WS-AMT = WS-P + WS-SI
    DISPLAY "Simple Interest: " WS-SI
    DISPLAY "Total Amount: " WS-AMT
    STOP RUN.
```

## Files to Create
- `simpleint.cbl` — your solution
- `test-input.txt` — three lines with test values (e.g., `10000`, `5.5`, `2`)