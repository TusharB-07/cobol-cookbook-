# Task 011: SRM-FOSS Game

**Tier:** 🥉 Bronze  
**Issue:** #16

## Task
Write a COBOL program that prints numbers 1 to 100, but:
- Multiples of 7 → print `SRM`
- Multiples of 11 → print `FOSS`
- Multiples of both 7 and 11 (i.e., 77) → print `SRMFOSS`
- Otherwise → print the number

## Acceptance Criteria (Exact Expected Output — First 20 Lines)
```
1
2
3
4
5
6
SRM
8
9
10
FOSS
12
13
SRM
15
16
17
18
19
FOSS
...
```
Full output should be 100 lines. Key lines to verify:
- Line 7: `SRM`
- Line 11: `FOSS`
- Line 14: `SRM`
- Line 21: `SRM`
- Line 22: `FOSS`
- Line 28: `SRM`
- Line 33: `FOSS`
- Line 35: `SRM`
- Line 42: `SRM`
- Line 44: `FOSS`
- Line 49: `SRM`
- Line 55: `FOSS`
- Line 56: `SRM`
- Line 63: `SRM`
- Line 66: `FOSS`
- Line 70: `SRM`
- Line 77: `SRMFOSS`
- Line 84: `SRM`
- Line 88: `FOSS`
- Line 91: `SRM`
- Line 98: `SRM`
- Line 99: `FOSS`

## Hints
- Same pattern as BizzBuzz but with 7 and 11
- `PERFORM VARYING WS-I FROM 1 BY 1 UNTIL WS-I > 100`
- Check both first (77), then 7, then 11

## Starter Skeleton
```cobol
IDENTIFICATION DIVISION.
PROGRAM-ID. SRMFOSS.
*> Author: <your-github-handle>
DATA DIVISION.
WORKING-STORAGE SECTION.
01 WS-I         PIC 9(3) VALUE 1.
01 WS-MOD7      PIC 9.
01 WS-MOD11     PIC 9.
PROCEDURE DIVISION.
    PERFORM VARYING WS-I FROM 1 BY 1 UNTIL WS-I > 100
        COMPUTE WS-MOD7 = FUNCTION MOD(WS-I, 7)
        COMPUTE WS-MOD11 = FUNCTION MOD(WS-I, 11)
        EVALUATE TRUE
            WHEN WS-MOD7 = 0 AND WS-MOD11 = 0
                DISPLAY "SRMFOSS"
            WHEN WS-MOD7 = 0
                DISPLAY "SRM"
            WHEN WS-MOD11 = 0
                DISPLAY "FOSS"
            WHEN OTHER
                DISPLAY WS-I
        END-EVALUATE
    END-PERFORM
    STOP RUN.
```

## Files to Create
- `srmfoss.cbl` — your solution
- (No `test-input.txt` needed)