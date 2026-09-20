# Task 001: BizzBuzz 1–50

**Tier:** 🥉 Bronze  
**Issue:** #6

## Task
Write a COBOL program that prints numbers 1 to 50, but:
- For multiples of 3, print `BIZZ`
- For multiples of 5, print `BUZZ`
- For multiples of both 3 and 5, print `BIZZBUZZ`
- Otherwise, print the number

## Acceptance Criteria (Exact Expected Output)
```
 1
 2
BIZZ
 4
BUZZ
BIZZ
 7
 8
BIZZ
BUZZ
11
BIZZ
13
14
BIZZBUZZ
16
17
BIZZ
19
BUZZ
BIZZ
22
23
BIZZ
BUZZ
26
BIZZ
28
29
BIZZBUZZ
31
32
BIZZ
34
BUZZ
BIZZ
37
38
BIZZ
BUZZ
41
BIZZ
43
44
BIZZBUZZ
46
47
BIZZ
49
BUZZ
```

## Hints
- Use `PERFORM VARYING` from 1 to 50
- Use `FUNCTION MOD(WS-I, 3)` and `FUNCTION MOD(WS-I, 5)` to check divisibility
- `EVALUATE TRUE` works well for multiple conditions
- Remember: check for both 3 and 5 *first* (BIZZBUZZ), then 3, then 5

## Starter Skeleton
```cobol
IDENTIFICATION DIVISION.
PROGRAM-ID. BIZZBUZZ.
*> Author: <your-github-handle>
DATA DIVISION.
WORKING-STORAGE SECTION.
01 WS-I        PIC 9(2) VALUE 1.
01 WS-I-DISP   PIC Z9.
01 WS-MOD3     PIC 9.
01 WS-MOD5     PIC 9.
PROCEDURE DIVISION.
    PERFORM VARYING WS-I FROM 1 BY 1 UNTIL WS-I > 50
        COMPUTE WS-MOD3 = FUNCTION MOD(WS-I, 3)
        COMPUTE WS-MOD5 = FUNCTION MOD(WS-I, 5)
        MOVE WS-I TO WS-I-DISP
        EVALUATE TRUE
            WHEN WS-MOD3 = 0 AND WS-MOD5 = 0
                DISPLAY "BIZZBUZZ"
            WHEN WS-MOD3 = 0
                DISPLAY "BIZZ"
            WHEN WS-MOD5 = 0
                DISPLAY "BUZZ"
            WHEN OTHER
                DISPLAY WS-I-DISP
        END-EVALUATE
    END-PERFORM
    STOP RUN.
```

## Files to Create
- `bizzbuzz.cbl` — your solution
- (No `test-input.txt` needed — program takes no input)