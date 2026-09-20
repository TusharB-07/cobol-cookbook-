# Task 020: Currency Converter

**Tier:** 🥈 Silver  
**Issue:** #25

## Task
Write a COBOL program that:
1. Has a lookup table of 3 exchange rates (base: INR)
   - USD: 83.50
   - EUR: 90.25
   - GBP: 105.75
2. Displays a menu to select target currency
3. Accepts an amount in INR
4. Converts and prints the result

## Acceptance Criteria (Exact Expected Output)

**Input:**
```
1
10000
```

**Output:**
```
Currency Converter (INR to...)
1. USD (83.50)
2. EUR (90.25)
3. GBP (105.75)
Enter choice: 1
Enter INR amount: 10000
10000.00 INR = 119.76 USD
```

**Input:**
```
2
50000
```

**Output:**
```
Currency Converter (INR to...)
1. USD (83.50)
2. EUR (90.25)
3. GBP (105.75)
Enter choice: 2
Enter INR amount: 50000
50000.00 INR = 554.02 EUR
```

## Hints
- Table for rates: `01 WS-RATES OCCURS 3 TIMES PIC 9(3)V99 VALUE 83.50 90.25 105.75`
- Currency names table: `01 WS-NAMES OCCURS 3 TIMES PIC X(3) VALUE "USD" "EUR" "GBP"`
- `EVALUATE WS-CHOICE` for menu
- `COMPUTE WS-RESULT = WS-INR / WS-RATES(WS-CHOICE)`

## Starter Skeleton
```cobol
IDENTIFICATION DIVISION.
PROGRAM-ID. CURRCONV.
*> Author: <your-github-handle>
DATA DIVISION.
WORKING-STORAGE SECTION.
01 WS-CHOICE    PIC 9.
01 WS-INR       PIC 9(7)V99.
01 WS-RESULT    PIC 9(7)V99.
01 WS-RATES     OCCURS 3 TIMES PIC 9(3)V99 VALUE 83.50 90.25 105.75.
01 WS-NAMES     OCCURS 3 TIMES PIC X(3) VALUE "USD" "EUR" "GBP".
PROCEDURE DIVISION.
    DISPLAY "Currency Converter (INR to...)"
    DISPLAY "1. USD (83.50)"
    DISPLAY "2. EUR (90.25)"
    DISPLAY "3. GBP (105.75)"
    DISPLAY "Enter choice: " WITH NO ADVANCING
    ACCEPT WS-CHOICE
    DISPLAY "Enter INR amount: " WITH NO ADVANCING
    ACCEPT WS-INR
    COMPUTE WS-RESULT = WS-INR / WS-RATES(WS-CHOICE)
    DISPLAY WS-INR " INR = " WS-RESULT " " WS-NAMES(WS-CHOICE)
    STOP RUN.
```

## Files to Create
- `currconv.cbl` — your solution
- `test-input.txt` — two lines (choice, amount) e.g., `1` then `10000`