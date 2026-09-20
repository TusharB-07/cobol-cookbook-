# Task 021: Report Generator

**Tier:** 🥇 Gold  
**Issue:** #26

## Task
Write a COBOL program that generates a formatted report with:
- Page header (repeated on each page)
- Detail lines (from input data)
- Page footer with page number
- Final grand totals

Input: Multiple records from stdin, each line: `Dept,Employee,Salary`
Simulate pagination: after every 5 detail lines, print footer + new header.

## Acceptance Criteria (Exact Expected Output)

**Input:**
```
IT,Alice,75000
IT,Bob,82000
HR,Carol,65000
HR,Dave,68000
Finance,Eve,90000
Finance,Frank,95000
IT,Grace,78000
HR,Henry,67000
Finance,Ivy,92000
Sales,Jack,55000
```

**Output:**
```
============================================================
                    SALARY REPORT - PAGE 1
============================================================
Dept       Employee    Salary
------------------------------------------------------------
IT         Alice       75000
IT         Bob         82000
HR         Carol       65000
HR         Dave        68000
Finance    Eve         90000
------------------------------------------------------------
Page Total:                           380000
============================================================
                    SALARY REPORT - PAGE 2
============================================================
Dept       Employee    Salary
------------------------------------------------------------
Finance    Frank       95000
IT         Grace       78000
HR         Henry       67000
Finance    Ivy         92000
Sales      Jack        55000
------------------------------------------------------------
Page Total:                           387000
============================================================
Grand Total:                          767000
Total Records: 10
```

## Hints
- Read all records into a table first (`OCCURS 50 TIMES`)
- Track line count, page count
- When `WS-LINE-COUNT = 5`, print footer, increment page, print header, reset line count
- `PIC 9(7)` for salary, `PIC 9(9)` for totals
- Build header/footer as separate paragraphs (`PERFORM PRINT-HEADER`)

## Starter Skeleton
```cobol
IDENTIFICATION DIVISION.
PROGRAM-ID. REPORTGEN.
*> Author: <your-github-handle>
DATA DIVISION.
WORKING-STORAGE SECTION.
01 WS-LINE       PIC X(80).
01 WS-DEPT       PIC X(15).
01 WS-EMP        PIC X(15).
01 WS-SAL        PIC 9(7).
01 WS-RECORDS    OCCURS 50 TIMES.
    05 WS-RDEPT     PIC X(15).
    05 WS-REMP      PIC X(15).
    05 WS-RSAL      PIC 9(7).
01 WS-COUNT      PIC 9(2) VALUE 0.
01 WS-I          PIC 9(2).
01 WS-PAGE       PIC 9(2) VALUE 1.
01 WS-LINE-CNT   PIC 9 VALUE 0.
01 WS-PAGE-TOT   PIC 9(9) VALUE 0.
01 WS-GRAND-TOT  PIC 9(9) VALUE 0.
PROCEDURE DIVISION.
    *> Read all records
    PERFORM UNTIL WS-LINE = SPACES
        ACCEPT WS-LINE
        IF WS-LINE NOT = SPACES
            ADD 1 TO WS-COUNT
            UNSTRING WS-LINE DELIMITED BY ","
                INTO WS-DEPT, WS-EMP, WS-SAL
            MOVE WS-DEPT TO WS-RDEPT(WS-COUNT)
            MOVE WS-EMP TO WS-REMP(WS-COUNT)
            MOVE WS-SAL TO WS-RSAL(WS-COUNT)
        END-IF
    END-PERFORM
    *> Generate report
    PERFORM PRINT-HEADER
    PERFORM VARYING WS-I FROM 1 BY 1 UNTIL WS-I > WS-COUNT
        *> Print detail, check pagination
    END-PERFORM
    PERFORM PRINT-FOOTER
    DISPLAY "Grand Total: " WS-GRAND-TOT
    DISPLAY "Total Records: " WS-COUNT
    STOP RUN.

PRINT-HEADER.
    DISPLAY "============================================================"
    DISPLAY "                    SALARY REPORT - PAGE " WS-PAGE
    DISPLAY "============================================================"
    DISPLAY "Dept       Employee    Salary"
    DISPLAY "------------------------------------------------------------"
    MOVE 0 TO WS-LINE-CNT, WS-PAGE-TOT.

PRINT-FOOTER.
    DISPLAY "------------------------------------------------------------"
    DISPLAY "Page Total:                           " WS-PAGE-TOT
    DISPLAY "============================================================".
```

## Files to Create
- `reportgen.cbl` — your solution
- `test-input.txt` — 10+ lines with test data (see example above), ending with blank line