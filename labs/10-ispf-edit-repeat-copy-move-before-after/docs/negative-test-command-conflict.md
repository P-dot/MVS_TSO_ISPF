# Negative Test Analysis — Command Conflict

## Attempt

The following line commands were prepared for one Enter:

```text
R  MULTI-R
C  MULTI-C
M  MULTI-M
A  MULTI-C-TARGET
B  MULTI-M-TARGET
```

## Observed result

```text
Command conflict
```

ISPF did not silently apply the intended composite mutation.

## Interpretation boundary

The evidence proves that this command set was rejected as conflicting in the observed ISPF 6.1 environment.

The screenshots do not prove the exact internal reason for the conflict, so the repository does not claim one.

## Recovery

```text
CANCEL
```

was issued.

A new Browse session confirmed the complete 28-record canonical baseline.

## Corrected test

The non-conflicting set:

```text
R  MULTI-R
C  MULTI-C
A  MULTI-C-TARGET
```

was prepared and executed with one Enter.

Observed working state:

- `MULTI-R` repeated;
- original `MULTI-C` preserved;
- copied `MULTI-C` placed after `MULTI-C-TARGET`;
- total records: 30.

The transaction was then cancelled and the 28-record baseline was independently revalidated.

## Result

```text
negative test: PASS
recovery: PASS
corrected execution: PASS
post-recovery validation: PASS
```
