# Task 022: FizzBuzz via JCL

**Tier:** 🥇 Gold  
**Issue:** #27

## Task
Create a JCL job that runs a COBOL FizzBuzz program (1-100, 3=FIZZ, 5=BUZZ, both=FIZZBUZZ).
The folder should contain:
1. `fizzbuzz.cbl` — the COBOL program
2. `fizzbuzz.jcl` — the JCL job
3. `README.md` — documentation explaining the JCL

## Acceptance Criteria
- COBOL program compiles and runs correctly (same logic as Task 001 but 1-100)
- JCL file has valid syntax for z/OS (JOB, EXEC, DD statements)
- README explains each JCL statement

## COBOL Program Expected Output (First 20 Lines)
```
1
2
FIZZ
4
BUZZ
FIZZ
7
8
FIZZ
BUZZ
11
FIZZ
13
14
FIZZBUZZ
16
17
FIZZ
19
BUZZ
...
```

## Hints
- COBOL: Same as BizzBuzz but 1-100 and FIZZ/BUZZ/FIZZBUZZ
- JCL structure:
  ```jcl
  //FIZZBUZZ JOB (ACCT),'FIZZBUZZ',CLASS=A,MSGCLASS=X
  //STEP1    EXEC PGM=COBOLC
  //SYSPRINT DD SYSOUT=*
  //SYSIN    DD *
        (COBOL source here)
  /*
  //LKED.SYSLMOD DD DSN=&&LOAD,FUNIT=SYSDA,SPACE=(CYL,(1,1))
  //GO.SYSOUT  DD SYSOUT=*
  ```
- For the workshop: document the JCL, actual z/OS execution is bonus

## Starter Skeleton (COBOL)
```cobol
IDENTIFICATION DIVISION.
PROGRAM-ID. FIZZBUZZ.
*> Author: <your-github-handle>
DATA DIVISION.
WORKING-STORAGE SECTION.
01 WS-I         PIC 9(3) VALUE 1.
01 WS-MOD3      PIC 9.
01 WS-MOD5      PIC 9.
PROCEDURE DIVISION.
    PERFORM VARYING WS-I FROM 1 BY 1 UNTIL WS-I > 100
        COMPUTE WS-MOD3 = FUNCTION MOD(WS-I, 3)
        COMPUTE WS-MOD5 = FUNCTION MOD(WS-I, 5)
        EVALUATE TRUE
            WHEN WS-MOD3 = 0 AND WS-MOD5 = 0
                DISPLAY "FIZZBUZZ"
            WHEN WS-MOD3 = 0
                DISPLAY "FIZZ"
            WHEN WS-MOD5 = 0
                DISPLAY "BUZZ"
            WHEN OTHER
                DISPLAY WS-I
        END-EVALUATE
    END-PERFORM
    STOP RUN.
```

## Starter Skeleton (JCL)
```jcl
//FIZZBUZZ JOB (ACCT),'FIZZBUZZ COBOL',CLASS=A,MSGCLASS=X
//COMPILE  EXEC PGM=IGYCRCTL,REGION=0M
//SYSPRINT DD SYSOUT=*
//SYSUT1   DD UNIT=SYSDA,SPACE=(CYL,(1,1))
//SYSUT2   DD UNIT=SYSDA,SPACE=(CYL,(1,1))
//SYSUT3   DD UNIT=SYSDA,SPACE=(CYL,(1,1))
//SYSUT4   DD UNIT=SYSDA,SPACE=(CYL,(1,1))
//SYSUT5   DD UNIT=SYSDA,SPACE=(CYL,(1,1))
//SYSUT6   DD UNIT=SYSDA,SPACE=(CYL,(1,1))
//SYSUT7   DD UNIT=SYSDA,SPACE=(CYL,(1,1))
//SYSLIN   DD DSN=&&LOADSET,DISP=(NEW,PASS),UNIT=SYSDA,
//            SPACE=(CYL,(1,1)),DCB=(RECFM=FB,LRECL=80,BLKSIZE=3200)
//SYSPUNCH DD DSN=&&LOADSET,DISP=(NEW,PASS),UNIT=SYSDA,
//            SPACE=(CYL,(1,1)),DCB=(RECFM=FB,LRECL=80,BLKSIZE=3200)
//SYSIN    DD *
       (COBOL source goes here)
/*
//LINK     EXEC PGM=IEWL,REGION=0M,COND=(0,NE,COMPILE)
//SYSPRINT DD SYSOUT=*
//SYSLMOD  DD DSN=&&LOADMOD,DISP=(NEW,PASS),UNIT=SYSDA,
//            SPACE=(CYL,(1,1)),DCB=(RECFM=U,BLKSIZE=32760)
//SYSUT1   DD UNIT=SYSDA,SPACE=(CYL,(1,1))
//SYSLIN   DD DSN=&&LOADSET,DISP=(OLD,DELETE)
//GO       EXEC PGM=*.LINK.SYSLMOD,COND=(0,NE,LINK)
//SYSOUT   DD SYSOUT=*
```

## Files to Create
- `fizzbuzz.cbl` — COBOL solution
- `fizzbuzz.jcl` — JCL job
- (No `test-input.txt` needed)