# Task 019: Palindrome Checker

**Tier:** 🥈 Silver  
**Issue:** #24

## Task
Write a COBOL program that:
1. Accepts a single word from the user (up to 30 chars, no spaces)
2. Checks if it's a palindrome (reads same forwards and backwards)
3. Case-insensitive comparison
4. Prints "Palindrome" or "Not a palindrome"

## Acceptance Criteria (Exact Expected Output)

**Input:** `RADAR`

**Output:**
```
Palindrome
```

**Input:** `Level`

**Output:**
```
Palindrome
```

**Input:** `COBOL`

**Output:**
```
Not a palindrome
```

**Input:** `A`

**Output:**
```
Palindrome
```

**Input:** `AB`

**Output:**
```
Not a palindrome
```

## Hints
- Convert to upper-case: `FUNCTION UPPER-CASE`
- Get length: `FUNCTION LENGTH-TRIM`
- Compare characters from both ends: `WS-I` from 1, `WS-J` from length
- Loop while `WS-I < WS-J`, if any mismatch → not palindrome

## Starter Skeleton
```cobol
IDENTIFICATION DIVISION.
PROGRAM-ID. PALINDRO.
*> Author: <your-github-handle>
DATA DIVISION.
WORKING-STORAGE SECTION.
01 WS-INPUT     PIC X(30).
01 WS-UPPER     PIC X(30).
01 WS-LEN       PIC 9(2).
01 WS-I         PIC 9(2).
01 WS-J         PIC 9(2).
01 WS-IS-PAL    PIC X(3) VALUE "YES".
PROCEDURE DIVISION.
    DISPLAY "Enter word: " WITH NO ADVANCING
    ACCEPT WS-INPUT
    MOVE FUNCTION UPPER-CASE(WS-INPUT) TO WS-UPPER
    COMPUTE WS-LEN = FUNCTION LENGTH-TRIM(WS-UPPER)
    MOVE 1 TO WS-I
    MOVE WS-LEN TO WS-J
    PERFORM UNTIL WS-I >= WS-J
        IF WS-UPPER(WS-I:1) NOT = WS-UPPER(WS-J:1)
            MOVE "NO" TO WS-IS-PAL
        END-IF
        ADD 1 TO WS-I
        SUBTRACT 1 FROM WS-J
    END-PERFORM
    IF WS-IS-PAL = "YES"
        DISPLAY "Palindrome"
    ELSE
        DISPLAY "Not a palindrome"
    END-IF
    STOP RUN.
```

## Files to Create
- `palindro.cbl` — your solution
- `test-input.txt` — one line with test word (e.g., `RADAR`)