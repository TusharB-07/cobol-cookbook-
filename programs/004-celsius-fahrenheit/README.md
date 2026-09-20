# Task 004: °C ↔ °F Converter

**Tier:** 🥉 Bronze  
**Issue:** #9

## Task
Write a COBOL program that:
1. Displays a menu: `1. C to F`, `2. F to C`
2. Accepts the user's choice (1 or 2)
3. Accepts the temperature value
4. Prints the converted value with formula shown

Formulas:
- `F = C × 9/5 + 32`
- `C = (F - 32) × 5/9`

## Acceptance Criteria (Exact Expected Output)

**Input:**
```
1
100
```

**Output:**
```
1. C to F
2. F to C
Enter choice: 1
Enter Celsius: 100
Formula: (100 * 9/5) + 32 = 212.00
212.00 °F
```

**Input:**
```
2
212
```

**Output:**
```
1. C to F
2. F to C
Enter choice: 2
Enter Fahrenheit: 212
Formula: (212 - 32) * 5/9 = 100.00
100.00 °C
```

## Hints
- Use `EVALUATE WS-CHOICE` for menu handling
- `PIC 9(3)V99` for temperature values
- `COMPUTE WS-RESULT = (WS-C * 9 / 5) + 32` — COBOL respects precedence
- Show the formula by building a string or displaying parts

## Starter Skeleton
```cobol
IDENTIFICATION DIVISION.
PROGRAM-ID. TEMPCONV.
*> Author: <your-github-handle>
DATA DIVISION.
WORKING-STORAGE SECTION.
01 WS-CHOICE    PIC 9.
01 WS-TEMP      PIC 9(3)V99.
01 WS-RESULT    PIC 9(3)V99.
PROCEDURE DIVISION.
    DISPLAY "1. C to F"
    DISPLAY "2. F to C"
    DISPLAY "Enter choice: " WITH NO ADVANCING
    ACCEPT WS-CHOICE
    EVALUATE WS-CHOICE
        WHEN 1
            DISPLAY "Enter Celsius: " WITH NO ADVANCING
            ACCEPT WS-TEMP
            COMPUTE WS-RESULT = (WS-TEMP * 9 / 5) + 32
            DISPLAY "Formula: (" WS-TEMP " * 9/5) + 32 = " WS-RESULT
            DISPLAY WS-RESULT " °F"
        WHEN 2
            DISPLAY "Enter Fahrenheit: " WITH NO ADVANCING
            ACCEPT WS-TEMP
            COMPUTE WS-RESULT = (WS-TEMP - 32) * 5 / 9
            DISPLAY "Formula: (" WS-TEMP " - 32) * 5/9 = " WS-RESULT
            DISPLAY WS-RESULT " °C"
        WHEN OTHER
            DISPLAY "Invalid choice"
    END-EVALUATE
    STOP RUN.
```

## Files to Create
- `tempconv.cbl` — your solution
- `test-input.txt` — two lines (choice, temperature) e.g., `1` then `100`