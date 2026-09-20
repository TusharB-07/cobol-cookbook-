# Task 013: Student Grades Report

**Tier:** 🥈 Silver  
**Issue:** #18

## Task
Write a COBOL program that:
1. Reads 5 student records from stdin (one per line)
2. Each record: `Name,Mark1,Mark2,Mark3` (comma-separated)
3. For each student: calculate average, assign grade
4. Print a formatted table

Grading:
- 90+ → A
- 80-89 → B
- 70-79 → C
- 60-69 → D
- Below 60 → F

## Acceptance Criteria (Exact Expected Output)

**Input:**
```
Alice,85,90,78
Bob,92,88,95
Carol,70,65,72
Dave,55,60,58
Eve,95,98,93
```

**Output:**
```
+--------+-------+-------+-------+--------+-------+
| Name   | Mark1 | Mark2 | Mark3 | Avg    | Grade |
+--------+-------+-------+-------+--------+-------+
| Alice  |    85 |    90 |    78 |  84.33 | B     |
| Bob    |    92 |    88 |    95 |  91.67 | A     |
| Carol  |    70 |    65 |    72 |  69.00 | D     |
| Dave   |    55 |    60 |    58 |  57.67 | F     |
| Eve    |    95 |    98 |    93 |  95.33 | A     |
+--------+-------+-------+-------+--------+-------+
```

## Hints
- Use `ACCEPT` in a loop 5 times
- Parse comma-separated input: `UNSTRING WS-LINE DELIMITED BY "," INTO WS-NAME WS-M1 WS-M2 WS-M3`
- Table for 5 students: `01 WS-STUDENTS OCCURS 5 TIMES` with sub-fields
- `COMPUTE WS-AVG = (WS-M1 + WS-M2 + WS-M3) / 3`
- `EVALUATE` for grade assignment
- Build table output with `DISPLAY` and careful spacing

## Starter Skeleton
```cobol
IDENTIFICATION DIVISION.
PROGRAM-ID. STUGRADE.
*> Author: <your-github-handle>
DATA DIVISION.
WORKING-STORAGE SECTION.
01 WS-LINE      PIC X(50).
01 WS-NAME      PIC X(10).
01 WS-M1        PIC 9(3).
01 WS-M2        PIC 9(3).
01 WS-M3        PIC 9(3).
01 WS-AVG       PIC 9(3)V99.
01 WS-GRADE     PIC X.
01 WS-I         PIC 9.
01 WS-STUDENT   OCCURS 5 TIMES.
    05 WS-SNAME     PIC X(10).
    05 WS-SM1       PIC 9(3).
    05 WS-SM2       PIC 9(3).
    05 WS-SM3       PIC 9(3).
    05 WS-SAVG      PIC 9(3)V99.
    05 WS-SGRADE    PIC X.
PROCEDURE DIVISION.
    DISPLAY "Enter 5 students (Name,Mark1,Mark2,Mark3):"
    PERFORM VARYING WS-I FROM 1 BY 1 UNTIL WS-I > 5
        ACCEPT WS-LINE
        UNSTRING WS-LINE DELIMITED BY ","
            INTO WS-NAME, WS-M1, WS-M2, WS-M3
        MOVE WS-NAME TO WS-SNAME(WS-I)
        MOVE WS-M1 TO WS-SM1(WS-I)
        MOVE WS-M2 TO WS-SM2(WS-I)
        MOVE WS-M3 TO WS-SM3(WS-I)
    END-PERFORM
    *> Process and display
    STOP RUN.
```

## Files to Create
- `stugrade.cbl` — your solution
- `test-input.txt` — 5 lines with test data (see example above)