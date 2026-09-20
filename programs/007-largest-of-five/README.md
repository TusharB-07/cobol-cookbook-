# Task 007: Largest of 5 Numbers

**Tier:** 🥉 Bronze  
**Issue:** #12

## Task
Write a COBOL program that:
1. Accepts 5 numbers from the user (one per line)
2. Stores them in a table/array
3. Uses `PERFORM VARYING` to find the largest
4. Prints the largest number

## Acceptance Criteria (Exact Expected Output)

**Input:**
```
12
45
7
89
23
```

**Output:**
```
Largest: 89
```

**Input:**
```
-5
-12
-3
-8
-1
```

**Output:**
```
Largest: -1
```

## Hints
- Define table: `01 WS-NUMS OCCURS 5 TIMES PIC S9(4)`
- Initialize `WS-MAX` with first element, then loop from 2 to 5
- `IF WS-NUMS(WS-I) > WS-MAX THEN MOVE WS-NUMS(WS-I) TO WS-MAX`

## Starter Skeleton
```cobol
IDENTIFICATION DIVISION.
PROGRAM-ID. LARGEST5.
*> Author: <your-github-handle>
DATA DIVISION.
WORKING-STORAGE SECTION.
01 WS-NUMS      OCCURS 5 TIMES PIC S9(4).
01 WS-MAX       PIC S9(4).
01 WS-I         PIC 9.
PROCEDURE DIVISION.
    PERFORM VARYING WS-I FROM 1 BY 1 UNTIL WS-I > 5
        DISPLAY "Enter number " WS-I ": " WITH NO ADVANCING
        ACCEPT WS-NUMS(WS-I)
    END-PERFORM
    MOVE WS-NUMS(1) TO WS-MAX
    PERFORM VARYING WS-I FROM 2 BY 1 UNTIL WS-I > 5
        IF WS-NUMS(WS-I) > WS-MAX
            MOVE WS-NUMS(WS-I) TO WS-MAX
        END-IF
    END-PERFORM
    DISPLAY "Largest: " WS-MAX
    STOP RUN.
```

## Files to Create
- `largest5.cbl` — your solution
- `test-input.txt` — five lines with test numbers (e.g., `12`, `45`, `7`, `89`, `23`)