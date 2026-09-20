# Task 005: Reverse String (No REVERSE Verb)

**Tier:** 🥉 Bronze  
**Issue:** #10

## Task
Write a COBOL program that:
1. Accepts a string from the user (up to 50 characters)
2. Prints the string reversed **without using the `REVERSE` intrinsic function**
3. Use a loop with array/table indexing

## Acceptance Criteria (Exact Expected Output)

**Input:** `HELLO`

**Output:**
```
Original: HELLO
Reversed: OLLEH
```

**Input:** `COBOL`

**Output:**
```
Original: COBOL
Reversed: LOBOC
```

**Input:** `A`

**Output:**
```
Original: A
Reversed: A
```

## Hints
- Define a table: `01 WS-CHAR OCCURS 50 TIMES PIC X`
- Move input string into the table character by character using `PERFORM VARYING`
- Build reversed string by reading table backwards
- Or: just display characters in reverse order directly in a loop
- `FUNCTION LENGTH-TRIM` to get actual input length

## Starter Skeleton
```cobol
IDENTIFICATION DIVISION.
PROGRAM-ID. REVSTR.
*> Author: <your-github-handle>
DATA DIVISION.
WORKING-STORAGE SECTION.
01 WS-INPUT     PIC X(50).
01 WS-REVERSED  PIC X(50).
01 WS-LEN       PIC 9(2).
01 WS-I         PIC 9(2).
01 WS-J         PIC 9(2).
01 WS-CHAR      OCCURS 50 TIMES PIC X.
PROCEDURE DIVISION.
    DISPLAY "Enter string: " WITH NO ADVANCING
    ACCEPT WS-INPUT
    COMPUTE WS-LEN = FUNCTION LENGTH-TRIM(WS-INPUT)
    *> Load into table
    PERFORM VARYING WS-I FROM 1 BY 1 UNTIL WS-I > WS-LEN
        MOVE WS-INPUT(WS-I:1) TO WS-CHAR(WS-I)
    END-PERFORM
    *> Build reversed
    MOVE 1 TO WS-J
    PERFORM VARYING WS-I FROM WS-LEN BY -1 UNTIL WS-I < 1
        MOVE WS-CHAR(WS-I) TO WS-REVERSED(WS-J:1)
        ADD 1 TO WS-J
    END-PERFORM
    DISPLAY "Original: " WS-INPUT(1:WS-LEN)
    DISPLAY "Reversed: " WS-REVERSED(1:WS-LEN)
    STOP RUN.
```

## Files to Create
- `revstr.cbl` — your solution
- `test-input.txt` — one line with test string (e.g., `HELLO`)