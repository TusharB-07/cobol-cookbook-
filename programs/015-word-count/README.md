# Task 015: Word Count

**Tier:** 🥈 Silver  
**Issue:** #20

## Task
Write a COBOL program that:
1. Accepts a sentence from the user (up to 200 chars)
2. Accepts a target word to search for
3. Counts how many times the target word appears (case-insensitive, whole word only)
4. Prints the count

## Acceptance Criteria (Exact Expected Output)

**Input:**
```
The quick brown fox jumps over the lazy dog
the
```

**Output:**
```
Word 'the' appears 2 times
```

**Input:**
```
COBOL is cool COBOL is powerful COBOL rocks
COBOL
```

**Output:**
```
Word 'COBOL' appears 3 times
```

**Input:**
```
Hello world
xyz
```

**Output:**
```
Word 'xyz' appears 0 times
```

## Hints
- Convert both sentence and target to upper-case: `FUNCTION UPPER-CASE`
- Parse sentence into words using `UNSTRING DELIMITED BY " "` (space)
- Store words in a table, loop and compare with target
- Or: use `INSPECT` with `TALLYING` for substring count, but need word boundaries

## Starter Skeleton
```cobol
IDENTIFICATION DIVISION.
PROGRAM-ID. WORDCNT.
*> Author: <your-github-handle>
DATA DIVISION.
WORKING-STORAGE SECTION.
01 WS-SENTENCE  PIC X(200).
01 WS-TARGET    PIC X(20).
01 WS-USENT     PIC X(200).
01 WS-UTARGET   PIC X(20).
01 WS-WORDS     OCCURS 50 TIMES PIC X(20).
01 WS-COUNT     PIC 9(3) VALUE 0.
01 WS-I         PIC 9(2).
01 WS-J         PIC 9(2).
01 WS-WORDCNT   PIC 9(2) VALUE 0.
PROCEDURE DIVISION.
    DISPLAY "Enter sentence: " WITH NO ADVANCING
    ACCEPT WS-SENTENCE
    DISPLAY "Enter target word: " WITH NO ADVANCING
    ACCEPT WS-TARGET
    MOVE FUNCTION UPPER-CASE(WS-SENTENCE) TO WS-USENT
    MOVE FUNCTION UPPER-CASE(WS-TARGET) TO WS-UTARGET
    *> Parse words
    UNSTRING WS-USENT DELIMITED BY " "
        INTO WS-WORDS(1) WS-WORDS(2) WS-WORDS(3) WS-WORDS(4) WS-WORDS(5)
             WS-WORDS(6) WS-WORDS(7) WS-WORDS(8) WS-WORDS(9) WS-WORDS(10)
    *> Count matches
    PERFORM VARYING WS-I FROM 1 BY 1 UNTIL WS-I > 10
        IF WS-WORDS(WS-I) = WS-UTARGET
            ADD 1 TO WS-COUNT
        END-IF
    END-PERFORM
    DISPLAY "Word '" WS-TARGET "' appears " WS-COUNT " times"
    STOP RUN.
```

## Files to Create
- `wordcnt.cbl` — your solution
- `test-input.txt` — two lines (sentence, then target word)