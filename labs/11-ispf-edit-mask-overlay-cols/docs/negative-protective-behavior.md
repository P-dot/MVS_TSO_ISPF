# Negative and Protective Behavior Analysis

## Block overlay setup conflict

During block overlay setup, ISPF displayed:

```text
Command conflict
```

The exact invalid pairing/state is not fully visible in evidence, so no unsupported root cause is claimed.

The sequence was corrected and block overlay completed successfully.

## MOVE + OVERLAY protection

Attempt:

```text
M  OVL-MOVE-SOURCE
O  OVL-MOVE-TARGET
```

Observed:

```text
Line not deleted
```

The source remained present.

Interpretation:

ISPF detected that not all source data could be placed over the target and protected the source from deletion.

## Recovery

The transaction was terminated with `CANCEL`.

Independent Browse returned to the canonical 12-record baseline.

## Result

```text
protective negative behavior: PASS
source preservation: PASS
rollback: PASS
post-recovery validation: PASS
```
