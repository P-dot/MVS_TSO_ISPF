# Technical Notes — Lab 10

## REPEAT semantics

`R3` repeats one source record three additional times.

This differs from count-based source commands such as `C2` and `M2`, where the number selects multiple consecutive source records.

## COPY semantics

COPY preserves the source and creates new records at a destination identified by `A` or `B`.

Validated:

- single record;
- numeric source count;
- block source;
- before/after destination.

## MOVE semantics

MOVE relocates records rather than preserving the source.

Validated:

- one record;
- two-record numeric source;
- block source;
- numeric destination repetition using `A2`.

## Pending state

The environment displayed:

```text
MOVE/COPY is pending
```

while a source operation awaited completion of its source/destination relationship.

This is documented as a valid intermediate editor state.

## Command conflict

A simultaneous set containing:

```text
R
C + A
M + B
```

returned:

```text
Command conflict
```

The evidence proves the conflict but does not prove a deeper internal parsing rule. No unsupported root cause is claimed.

The lab recovered using `CANCEL`, independently verified the 28-record baseline, then retried a simpler non-conflicting set:

```text
R
C + A
```

which completed successfully with one Enter and produced the predicted 30-record working state.

## M3 rationale

The lab began as an M2 operational capability.

Execution produced stronger evidence:

- multiple controlled mutation transactions;
- pending-state observation;
- real command-conflict negative test;
- explicit rollback;
- corrected execution;
- independent post-recovery verification.

Therefore the final maturity is M3 — Resilient.
