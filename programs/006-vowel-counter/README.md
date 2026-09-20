# Task 006: Vowel Counter

**Tier:** 🥉 Bronze  
**Issue:** #11

## Task
Write a COBOL program that:
1. Accepts a sentence from the user (up to 100 characters)
2. Counts the number of vowels (A, E, I, O, U — case insensitive)
3. Prints the count

## Acceptance Criteria (Exact Expected Output)

**Input:** `Hello World`

**Output:**
```
Vowel count: 3
```

**Input:** `COBOL IS COOL`

**Output:**
```
Vowel count: 4
```

**Input:** `XYZ`

**Output:**
```
Vowel count: 0
```

## Hints
- Use `FUNCTION UPPER-CASE` to normalize, or check both upper and lower
- Define a table of vowels: `01 WS-VOWELS OCCURS 5 TIMES PIC X VALUE "A", "E", "I", "O", "U"`
- Loop through each character of input, loop through vowel table to check match
- `FUNCTION LENGTH-TRIM` for actual length

## Starter Skeleton
```cobol
IDENTIFICATION DIVISION.
PROGRAM-ID. VOWELCNT.
*> Author: <your-github-handle>
DATA DIVISION.
WORKING-STORAGE SECTION.
01 WS-INPUT     PIC X(100).
01 WS-LEN       PIC 9(3).
01 WS-I         PIC 9(3).
01 WS-J         PIC 9.
01 WS-COUNT     PIC 9(3) VALUE 0.
01 WS-CHAR      PIC X.
01 WS-VOWELS    OCCURS 5 TIMES PIC X VALUE "A" "E" "I" "O" "U".
PROCEDURE DIVISION.
    DISPLAY "Enter sentence: " WITH NO ADVANCING
    ACCEPT WS-INPUT
    COMPUTE WS-LEN = FUNCTION LENGTH-TRIM(WS-INPUT)
    PERFORM VARYING WS-I FROM 1 BY 1 UNTIL WS-I > WS-LEN
        MOVE FUNCTION UPPER-CASE(WS-INPUT(WS-I:1)) TO WS-CHAR
        PERFORM VARYING WS-J FROM 1 BY 1 UNTIL WS-J > 5
            IF WS-CHAR = WS-VOWELS(WS-J)
                ADD 1 TO WS-COUNT
            END-IF
        END-PERFORM
    END-PERFORM
    DISPLAY "Vowel count: " WS-COUNT
    STOP RUN.
```

## Files to Create
- `vowelcnt.cbl` — your solution
- `test-input.txt` — one line with test sentence (e.g., `Hello World`)