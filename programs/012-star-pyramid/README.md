# Task 012: Star Pyramid

**Tier:** 🥉 Bronze  
**Issue:** #17

## Task
Write a COBOL program that prints a centered star pyramid with 5 rows.

## Acceptance Criteria (Exact Expected Output)
```
    *
   ***
  *****
 *******
*********
```
(Each row has 2 more stars than the previous, centered in a width of 9)

## Hints
- Outer loop: rows 1 to 5
- Stars per row = `2 * row - 1`
- Spaces before stars = `5 - row`
- Use `PERFORM VARYING` for rows, inner loops for spaces and stars
- Or build each line in a variable using `STRING` / `FUNCTION REPEAT`

## Starter Skeleton
```cobol
IDENTIFICATION DIVISION.
PROGRAM-ID. STARPYR.
*> Author: <your-github-handle>
DATA DIVISION.
WORKING-STORAGE SECTION.
01 WS-ROW       PIC 9.
01 WS-SPACES    PIC 9.
01 WS-STARS     PIC 9.
01 WS-LINE      PIC X(20).
01 WS-I         PIC 9.
PROCEDURE DIVISION.
    PERFORM VARYING WS-ROW FROM 1 BY 1 UNTIL WS-ROW > 5
        COMPUTE WS-SPACES = 5 - WS-ROW
        COMPUTE WS-STARS = 2 * WS-ROW - 1
        MOVE SPACES TO WS-LINE
        PERFORM VARYING WS-I FROM 1 BY 1 UNTIL WS-I > WS-SPACES
            STRING WS-LINE " " INTO WS-LINE
        END-PERFORM
        PERFORM VARYING WS-I FROM 1 BY 1 UNTIL WS-I > WS-STARS
            STRING WS-LINE "*" INTO WS-LINE
        END-PERFORM
        DISPLAY WS-LINE
    END-PERFORM
    STOP RUN.
```

## Files to Create
- `starpyr.cbl` — your solution
- (No `test-input.txt` needed)