# Task 018: Week's Temperatures

**Tier:** 🥈 Silver  
**Issue:** #23

## Task
Write a COBOL program that:
1. Reads 7 temperature values (one per day, one per line)
2. Stores them in a table
3. Calculates and prints: minimum, maximum, average (2 decimal places)

## Acceptance Criteria (Exact Expected Output)

**Input:**
```
22.5
24.0
21.5
25.5
23.0
22.0
24.5
```

**Output:**
```
Min: 21.50
Max: 25.50
Avg: 23.29
```

**Input:**
```
30
32
28
31
29
33
27
```

**Output:**
```
Min: 27.00
Max: 33.00
Avg: 30.00
```

## Hints
- Table: `01 WS-TEMPS OCCURS 7 TIMES PIC 9(2)V99`
- Initialize `WS-MIN` and `WS-MAX` with first element
- Loop to find min/max and sum
- `COMPUTE WS-AVG = WS-SUM / 7`

## Starter Skeleton
```cobol
IDENTIFICATION DIVISION.
PROGRAM-ID. WEEKTEMP.
*> Author: <your-github-handle>
DATA DIVISION.
WORKING-STORAGE SECTION.
01 WS-TEMPS     OCCURS 7 TIMES PIC 9(2)V99.
01 WS-MIN       PIC 9(2)V99.
01 WS-MAX       PIC 9(2)V99.
01 WS-SUM       PIC 9(4)V99 VALUE 0.
01 WS-AVG       PIC 9(2)V99.
01 WS-I         PIC 9.
PROCEDURE DIVISION.
    DISPLAY "Enter 7 temperatures:"
    PERFORM VARYING WS-I FROM 1 BY 1 UNTIL WS-I > 7
        DISPLAY "Day " WS-I ": " WITH NO ADVANCING
        ACCEPT WS-TEMPS(WS-I)
        ADD WS-TEMPS(WS-I) TO WS-SUM
    END-PERFORM
    MOVE WS-TEMPS(1) TO WS-MIN, WS-MAX
    PERFORM VARYING WS-I FROM 2 BY 1 UNTIL WS-I > 7
        IF WS-TEMPS(WS-I) < WS-MIN
            MOVE WS-TEMPS(WS-I) TO WS-MIN
        END-IF
        IF WS-TEMPS(WS-I) > WS-MAX
            MOVE WS-TEMPS(WS-I) TO WS-MAX
        END-IF
    END-PERFORM
    COMPUTE WS-AVG = WS-SUM / 7
    DISPLAY "Min: " WS-MIN
    DISPLAY "Max: " WS-MAX
    DISPLAY "Avg: " WS-AVG
    STOP RUN.
```

## Files to Create
- `weektemp.cbl` — your solution
- `test-input.txt` — 7 lines with test temperatures (e.g., `22.5`, `24.0`, `21.5`, `25.5`, `23.0`, `22.0`, `24.5`)