# Task 023: COBOL vs Python

**Tier:** 🥇 Gold  
**Issue:** #28

## Task
Implement the **same task** in both COBOL and Python, then write a comparison README.

**Task:** Read 10 integers from stdin, print the sum, average (2 decimals), minimum, and maximum.

## Acceptance Criteria

Both programs must produce identical output for the same input.

**Input:**
```
12
45
7
89
23
56
34
78
91
11
```

**Output (both programs):**
```
Sum: 446
Avg: 44.60
Min: 7
Max: 91
```

## Files to Create
- `stats.cbl` — COBOL solution
- `stats.py` — Python solution
- `comparison.md` — Comparison document

## Comparison.md Template
```markdown
# COBOL vs Python: Statistics Calculator

## Task
Read 10 integers, compute sum, average, min, max.

## Code Comparison

| Aspect | COBOL | Python |
|--------|-------|--------|
| Lines of code | ~35 | ~8 |
| Variable declaration | Required (PIC clauses) | Dynamic |
| Loop syntax | `PERFORM VARYING` | `for` / `while` |
| Input handling | `ACCEPT` per line | `input()` or `sys.stdin` |
| Output formatting | `PIC` / `DISPLAY` | f-strings / `format()` |
| Type safety | Strict (compile-time) | Dynamic (runtime) |

## COBOL Code
```cobol
*[paste your COBOL code here]*
```

## Python Code
```python
#[paste your Python code here]#
```

## Observations
- **Verbosity**: COBOL requires explicit declarations; Python is concise
- **Readability**: COBOL reads like English; Python reads like pseudocode
- **Performance**: COBOL compiled; Python interpreted (but negligible here)
- **Error handling**: COBOL compile errors vs Python runtime errors
- **Learning curve**: COBOL DIVISION/SECTION structure vs Python's flat script

## Verdict
COBOL excels at: _______________
Python excels at: _______________
```

## Starter Skeleton (COBOL)
```cobol
IDENTIFICATION DIVISION.
PROGRAM-ID. STATS.
*> Author: <your-github-handle>
DATA DIVISION.
WORKING-STORAGE SECTION.
01 WS-NUMS      OCCURS 10 TIMES PIC S9(4).
01 WS-SUM       PIC S9(6) VALUE 0.
01 WS-MIN       PIC S9(4).
01 WS-MAX       PIC S9(4).
01 WS-AVG       PIC 9(3)V99.
01 WS-I         PIC 9(2).
PROCEDURE DIVISION.
    PERFORM VARYING WS-I FROM 1 BY 1 UNTIL WS-I > 10
        ACCEPT WS-NUMS(WS-I)
        ADD WS-NUMS(WS-I) TO WS-SUM
    END-PERFORM
    MOVE WS-NUMS(1) TO WS-MIN, WS-MAX
    PERFORM VARYING WS-I FROM 2 BY 1 UNTIL WS-I > 10
        IF WS-NUMS(WS-I) < WS-MIN
            MOVE WS-NUMS(WS-I) TO WS-MIN
        END-IF
        IF WS-NUMS(WS-I) > WS-MAX
            MOVE WS-NUMS(WS-I) TO WS-MAX
        END-IF
    END-PERFORM
    COMPUTE WS-AVG = WS-SUM / 10
    DISPLAY "Sum: " WS-SUM
    DISPLAY "Avg: " WS-AVG
    DISPLAY "Min: " WS-MIN
    DISPLAY "Max: " WS-MAX
    STOP RUN.
```

## Starter Skeleton (Python)
```python
#!/usr/bin/env python3
nums = []
for _ in range(10):
    nums.append(int(input()))
print(f"Sum: {sum(nums)}")
print(f"Avg: {sum(nums)/10:.2f}")
print(f"Min: {min(nums)}")
print(f"Max: {max(nums)}")
```

## Files to Create
- `stats.cbl` — COBOL solution
- `stats.py` — Python solution
- `comparison.md` — Your filled comparison
- `test-input.txt` — 10 lines with test numbers (see example above)