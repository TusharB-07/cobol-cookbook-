# Task 017: Inventory Report

**Tier:** 🥈 Silver  
**Issue:** #22

## Task
Write a COBOL program that:
1. Reads inventory lines from stdin until EOF (or empty line)
2. Each line: `ItemName,Quantity,UnitPrice` (comma-separated)
3. For each item: calculate line total = Quantity × UnitPrice
4. Print a formatted report with line totals and grand total

## Acceptance Criteria (Exact Expected Output)

**Input:**
```
Laptop,5,45000.00
Mouse,20,800.00
Keyboard,10,1500.00
Monitor,3,12000.00
```

**Output:**
```
+----------+----------+------------+------------+
| Item     | Qty      | Unit Price | Line Total |
+----------+----------+------------+------------+
| Laptop   |        5 |   45000.00 |  225000.00 |
| Mouse    |       20 |     800.00 |   16000.00 |
| Keyboard |       10 |    1500.00 |   15000.00 |
| Monitor  |        3 |   12000.00 |   36000.00 |
+----------+----------+------------+------------+
| Grand Total                              |  292000.00 |
+------------------------------------------+------------+
```

## Hints
- Read in a loop until `AT END` or empty line
- Table with `OCCURS 20 TIMES` (max items)
- `UNSTRING` for parsing
- `COMPUTE WS-LINE-TOTAL = WS-QTY * WS-PRICE`
- Accumulate `WS-GRAND-TOTAL`
- Format with `PIC 9(9)V99` for currency

## Starter Skeleton
```cobol
IDENTIFICATION DIVISION.
PROGRAM-ID. INVRPT.
*> Author: <your-github-handle>
DATA DIVISION.
WORKING-STORAGE SECTION.
01 WS-LINE       PIC X(80).
01 WS-ITEM       PIC X(15).
01 WS-QTY        PIC 9(4).
01 WS-PRICE      PIC 9(7)V99.
01 WS-LTOTAL     PIC 9(9)V99.
01 WS-GTOTAL     PIC 9(9)V99 VALUE 0.
01 WS-COUNT      PIC 9(2) VALUE 0.
01 WS-I          PIC 9(2).
01 WS-INV        OCCURS 20 TIMES.
    05 WS-INAME     PIC X(15).
    05 WS-IQTY      PIC 9(4).
    05 WS-IPRICE    PIC 9(7)V99.
    05 WS-ILTOTAL   PIC 9(9)V99.
PROCEDURE DIVISION.
    DISPLAY "Enter inventory (Item,Qty,Price), blank to end:"
    PERFORM UNTIL WS-LINE = SPACES
        ACCEPT WS-LINE
        IF WS-LINE NOT = SPACES
            ADD 1 TO WS-COUNT
            UNSTRING WS-LINE DELIMITED BY ","
                INTO WS-ITEM, WS-QTY, WS-PRICE
            MOVE WS-ITEM TO WS-INAME(WS-COUNT)
            MOVE WS-QTY TO WS-IQTY(WS-COUNT)
            MOVE WS-PRICE TO WS-IPRICE(WS-COUNT)
            COMPUTE WS-LTOTAL = WS-QTY * WS-PRICE
            MOVE WS-LTOTAL TO WS-ILTOTAL(WS-COUNT)
            ADD WS-LTOTAL TO WS-GTOTAL
        END-IF
    END-PERFORM
    *> Print report
    STOP RUN.
```

## Files to Create
- `invrpt.cbl` — your solution
- `test-input.txt` — 4+ lines with test data (see example above), ending with blank line