# Task 025: Caesar Cipher

**Tier:** 🥇 Gold  
**Issue:** #30

## Task
Write a COBOL program that:
1. Accepts a mode: `E` for encrypt, `D` for decrypt
2. Accepts a shift value (1-25)
3. Accepts a message (uppercase A-Z only, up to 100 chars)
4. Applies Caesar cipher and prints result

Encryption: shift each letter forward by N positions (wrap Z→A)
Decryption: shift each letter backward by N positions (wrap A→Z)

## Acceptance Criteria (Exact Expected Output)

**Input:**
```
E
3
HELLO
```

**Output:**
```
KHOOR
```

**Input:**
```
D
3
KHOOR
```

**Output:**
```
HELLO
```

**Input:**
```
E
1
XYZ
```

**Output:**
```
YZA
```

**Input:**
```
D
5
COBOL
```

**Output:**
```
XJWJG
```

## Hints
- Work with uppercase only: `FUNCTION UPPER-CASE`
- Convert char to ordinal: `FUNCTION ORD(WS-CHAR)` — 'A' = 65
- Shift: `(ORD - 65 + SHIFT) MOD 26 + 65` for encrypt
- Decrypt: `(ORD - 65 - SHIFT + 26) MOD 26 + 65`
- Convert back: `FUNCTION CHAR(WS-NEW-ORD)`
- Loop through each character of message

## Starter Skeleton
```cobol
IDENTIFICATION DIVISION.
PROGRAM-ID. CAESAR.
*> Author: <your-github-handle>
DATA DIVISION.
WORKING-STORAGE SECTION.
01 WS-MODE      PIC X.
01 WS-SHIFT     PIC 9(2).
01 WS-MSG       PIC X(100).
01 WS-RESULT    PIC X(100).
01 WS-LEN       PIC 9(3).
01 WS-I         PIC 9(3).
01 WS-CHAR      PIC X.
01 WS-ORD       PIC 9(3).
01 WS-NEW-ORD   PIC 9(3).
PROCEDURE DIVISION.
    DISPLAY "Mode (E/D): " WITH NO ADVANCING
    ACCEPT WS-MODE
    DISPLAY "Shift (1-25): " WITH NO ADVANCING
    ACCEPT WS-SHIFT
    DISPLAY "Message: " WITH NO ADVANCING
    ACCEPT WS-MSG
    MOVE FUNCTION UPPER-CASE(WS-MSG) TO WS-MSG
    COMPUTE WS-LEN = FUNCTION LENGTH-TRIM(WS-MSG)
    PERFORM VARYING WS-I FROM 1 BY 1 UNTIL WS-I > WS-LEN
        MOVE WS-MSG(WS-I:1) TO WS-CHAR
        IF WS-CHAR >= "A" AND WS-CHAR <= "Z"
            COMPUTE WS-ORD = FUNCTION ORD(WS-CHAR)
            IF WS-MODE = "E"
                COMPUTE WS-NEW-ORD = (WS-ORD - 65 + WS-SHIFT) MOD 26 + 65
            ELSE
                COMPUTE WS-NEW-ORD = (WS-ORD - 65 - WS-SHIFT + 26) MOD 26 + 65
            END-IF
            MOVE FUNCTION CHAR(WS-NEW-ORD) TO WS-RESULT(WS-I:1)
        ELSE
            MOVE WS-CHAR TO WS-RESULT(WS-I:1)
        END-IF
    END-PERFORM
    DISPLAY WS-RESULT(1:WS-LEN)
    STOP RUN.
```

## Files to Create
- `caesar.cbl` — your solution
- `test-input.txt` — three lines (mode, shift, message) e.g., `E`, `3`, `HELLO`