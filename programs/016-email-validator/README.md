# Task 016: Toy Email Validator

**Tier:** 🥈 Silver  
**Issue:** #21

## Task
Write a COBOL program that:
1. Accepts an email address from the user
2. Validates it has:
   - Exactly one `@` symbol
   - At least one `.` after the `@`
   - Non-empty local part (before @)
   - Non-empty domain part (after @, before last .)
3. Prints "Valid" or "Invalid"

## Acceptance Criteria (Exact Expected Output)

**Input:** `user@example.com`

**Output:**
```
Valid
```

**Input:** `user@.com`

**Output:**
```
Invalid
```

**Input:** `userexample.com`

**Output:**
```
Invalid
```

**Input:** `@example.com`

**Output:**
```
Invalid
```

**Input:** `user@domain`

**Output:**
```
Invalid
```

**Input:** `user@domain.co.uk`

**Output:**
```
Valid
```

## Hints
- Use `INSPECT WS-EMAIL TALLYING WS-AT-COUNT FOR ALL "@"` to count @ symbols
- Find position of `@` and `.` using `FUNCTION FIND` or manual loop
- Check substring after `@` contains `.`

## Starter Skeleton
```cobol
IDENTIFICATION DIVISION.
PROGRAM-ID. EMAILVAL.
*> Author: <your-github-handle>
DATA DIVISION.
WORKING-STORAGE SECTION.
01 WS-EMAIL      PIC X(50).
01 WS-AT-COUNT   PIC 9.
01 WS-DOT-COUNT  PIC 9.
01 WS-AT-POS     PIC 9(2).
01 WS-DOT-POS    PIC 9(2).
01 WS-I          PIC 9(2).
01 WS-VALID      PIC X(7) VALUE "Valid".
PROCEDURE DIVISION.
    DISPLAY "Enter email: " WITH NO ADVANCING
    ACCEPT WS-EMAIL
    INSPECT WS-EMAIL TALLYING WS-AT-COUNT FOR ALL "@"
    INSPECT WS-EMAIL TALLYING WS-DOT-COUNT FOR ALL "."
    IF WS-AT-COUNT NOT = 1
        MOVE "Invalid" TO WS-VALID
    ELSE
        *> Find @ position
        PERFORM VARYING WS-I FROM 1 BY 1 UNTIL WS-I > FUNCTION LENGTH(WS-EMAIL)
            IF WS-EMAIL(WS-I:1) = "@"
                MOVE WS-I TO WS-AT-POS
            END-IF
        END-PERFORM
        *> Check dot after @
        PERFORM VARYING WS-I FROM WS-AT-POS BY 1 UNTIL WS-I > FUNCTION LENGTH(WS-EMAIL)
            IF WS-EMAIL(WS-I:1) = "."
                MOVE WS-I TO WS-DOT-POS
            END-IF
        END-PERFORM
        IF WS-DOT-POS = 0 OR WS-AT-POS = 1 OR WS-AT-POS = FUNCTION LENGTH(WS-EMAIL)
            MOVE "Invalid" TO WS-VALID
        END-IF
    END-IF
    DISPLAY WS-VALID
    STOP RUN.
```

## Files to Create
- `emailval.cbl` — your solution
- `test-input.txt` — one line with test email (e.g., `user@example.com`)