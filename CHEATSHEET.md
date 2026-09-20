# COBOL Quick Reference Cheat Sheet
*SRM FOSS Club × IBM Z Workshop — 21 Sept 2026*

---

## Program Structure
```cobol
IDENTIFICATION DIVISION.
PROGRAM-ID. MYPROG.
DATA DIVISION.
WORKING-STORAGE SECTION.
    *> variables here
PROCEDURE DIVISION.
    *> code here
    STOP RUN.
```

---

## Variables (PICTURE Clauses)
| Type | Example | Meaning |
|------|---------|---------|
| `PIC 9(4)` | 4-digit integer | `9` = digit, `(4)` = 4 times |
| `PIC S9(4)` | Signed integer | `S` = sign |
| `PIC 9(5)V99` | 5 digits, 2 decimals | `V` = implied decimal point |
| `PIC X(20)` | 20-char string | `X` = any character |
| `PIC X(10) VALUE "HELLO"` | With initial value | |

---

## Input / Output
```cobol
DISPLAY "Prompt: " WITH NO ADVANCING   *> no newline
ACCEPT WS-VAR                          *> read into variable
DISPLAY WS-VAR                         *> print variable
DISPLAY "Value: " WS-VAR               *> concatenate
```

---

## Arithmetic
```cobol
COMPUTE WS-RESULT = WS-A + WS-B        *> add
COMPUTE WS-RESULT = WS-A - WS-B        *> subtract
COMPUTE WS-RESULT = WS-A * WS-B        *> multiply
COMPUTE WS-RESULT = WS-A / WS-B        *> divide
COMPUTE WS-RESULT = (WS-A + WS-B) / 2  *> expressions OK
```
> Use `PIC 9(n)V99` for decimal results

---

## Conditionals
```cobol
IF WS-A > WS-B
    DISPLAY "A greater"
ELSE
    DISPLAY "B greater or equal"
END-IF

EVALUATE WS-CHOICE
    WHEN 1
        DISPLAY "One"
    WHEN 2
        DISPLAY "Two"
    WHEN OTHER
        DISPLAY "Other"
END-EVALUATE
```

---

## Loops
```cobol
*> Fixed count
PERFORM VARYING WS-I FROM 1 BY 1 UNTIL WS-I > 10
    DISPLAY WS-I
END-PERFORM

*> Until condition
PERFORM UNTIL WS-DONE = "Y"
    *> loop body
END-PERFORM
```

---

## Tables (Arrays)
```cobol
01 WS-NUMS OCCURS 10 TIMES PIC 9(3).
01 WS-NAMES OCCURS 5 TIMES  PIC X(15) VALUE "A" "B" "C" "D" "E".

MOVE 42 TO WS-NUMS(3)           *> set element 3
DISPLAY WS-NAMES(2)             *> get element 2
PERFORM VARYING WS-I FROM 1 BY 1 UNTIL WS-I > 10
    DISPLAY WS-NUMS(WS-I)
END-PERFORM
```

---

## String Handling
```cobol
STRING WS-A " " WS-B DELIMITED BY SIZE INTO WS-RESULT
UNSTRING WS-LINE DELIMITED BY "," INTO WS-F1 WS-F2 WS-F3
MOVE FUNCTION UPPER-CASE(WS-STR) TO WS-UPPER
MOVE FUNCTION LOWER-CASE(WS-STR) TO WS-LOWER
COMPUTE WS-LEN = FUNCTION LENGTH-TRIM(WS-STR)
MOVE FUNCTION ORD("A") TO WS-N        *> 65
MOVE FUNCTION CHAR(65) TO WS-CH       *> "A"
```

---

## Math Functions
```cobol
FUNCTION MOD(WS-A, WS-B)              *> remainder
FUNCTION MAX(WS-A, WS-B, WS-C)        *> maximum
FUNCTION MIN(WS-A, WS-B)              *> minimum
FUNCTION SQRT(WS-N)                   *> square root
```

---

## Common Patterns

**Find max in table:**
```cobol
MOVE WS-TABLE(1) TO WS-MAX
PERFORM VARYING WS-I FROM 2 BY 1 UNTIL WS-I > 10
    IF WS-TABLE(WS-I) > WS-MAX
        MOVE WS-TABLE(WS-I) TO WS-MAX
    END-IF
END-PERFORM
```

**Sum of digits (string method):**
```cobol
PERFORM VARYING WS-I FROM 1 BY 1 UNTIL WS-I > WS-LEN
    MOVE WS-STR(WS-I:1) TO WS-DIGIT
    ADD WS-DIGIT TO WS-SUM
END-PERFORM
```

**Parse comma-separated line:**
```cobol
UNSTRING WS-LINE DELIMITED BY ","
    INTO WS-FIELD1, WS-FIELD2, WS-FIELD3
```

---

## Compile & Run (GnuCOBOL)
```bash
cobc -x -free myprog.cbl -o myprog
./myprog
# With input file:
./myprog < test-input.txt
```

---

## PR Checklist
- [ ] Code compiles: `cobc -x -free prog.cbl -o prog`
- [ ] Output matches issue exactly
- [ ] `test-input.txt` included if program reads stdin
- [ ] PR description references issue: `Fixes #001`

---

## Need Help?
- **Table Captain** — Git/COBOL unblocking
- **Reviewer Desk** — PR review, merge guidance
- **GitHub Help Desk** — Account, auth, setup issues

*Keep this sheet handy! 🚀*