# Lab 10 — ISPF Edit Line Commands: Repeat, Copy, Move, Before and After

## Architecture metadata

```yaml
lab:
  historical_id: "labs/10-ispf-edit-repeat-copy-move-before-after"
  status: "VALIDATED"

architecture:
  domain: "Operations and Service Management"
  capability: "Controlled ISPF Edit record replication, relocation and multi-command execution"
  lifecycle:
    - Baseline
    - Operate
    - Observe
    - Diagnose
    - Recover
  maturity: "M3 — Resilient"
  integration_level: "I0 — Standalone"
```

## Objective

Validate Bosler Chapter 12 Edit line-command semantics using a deterministic 28-record repository-owned fixture.

The lab proves:

- Repeat — single, numeric and block;
- Copy — single, numeric and block;
- Move — single, numeric and block;
- `A` / `B` destination semantics;
- numeric destination repetition with `A2`;
- pending MOVE/COPY state;
- multiple line commands;
- controlled conflict handling;
- rollback after every mutation transaction;
- final independent baseline verification.

## Fixture

```text
IBMUSER.ISPF.LAB(EDIT10)
```

Canonical repository copy:

```text
fixtures/edit/EDIT10-baseline.txt
```

Baseline:

```text
28 records
```

## REPEAT validation

```text
R       28 -> 29
R3      29 -> 32
RR/RR   32 -> 34
CANCEL  34 -> persistent 28
```

`R3` means repeat one source line three additional times.

The `RR/RR` block retained source order.

## COPY validation

```text
C + A       28 -> 29
C2 + B      29 -> 31
CC/CC + A   31 -> 33
CANCEL      -> persistent 28
```

COPY retained the source and created destination copies.

During block COPY the environment exposed:

```text
MOVE/COPY is pending
```

before the source/destination relationship was completed.

## MOVE validation

```text
M + B       28 -> 28
M2 + A2     28 -> 30
MM/MM + B   30 -> 30
CANCEL      -> persistent 28
```

MOVE removed the source from its original position.

`A2` repeated the moved two-record payload twice at the destination, so the working record count increased by two.

## Multiple-command negative test

A composite one-Enter command set was prepared:

```text
R  MULTI-R
C  MULTI-C
M  MULTI-M
A  MULTI-C-TARGET
B  MULTI-M-TARGET
```

Observed:

```text
Command conflict
```

The exact internal cause is not inferred beyond the observed conflict.

`CANCEL` was issued and a new Browse session verified the 28-record baseline.

## Corrected multiple-command execution

A smaller command set was then prepared:

```text
R  MULTI-R
C  MULTI-C
A  MULTI-C-TARGET
```

and executed with one Enter.

Observed:

- `MULTI-R` repeated;
- source `MULTI-C` remained;
- copy of `MULTI-C` appeared after `MULTI-C-TARGET`;
- working record count = 30.

The transaction was cancelled and the final independent Browse showed the canonical 28-record baseline.

## Validation summary

| Capability | Result |
|---|---|
| REPEAT | PASS |
| COPY | PASS |
| MOVE | PASS |
| A/B destination semantics | PASS |
| numeric destination repetition | PASS |
| pending MOVE/COPY state | PASS |
| command-conflict negative test | PASS |
| conflict recovery | PASS |
| corrected multi-command execution | PASS |
| rollback after mutation | PASS |
| final persistent state | 28-record baseline restored |

## Failure / exception analysis

The real `Command conflict` is retained as first-class evidence.

This is not hidden as a failed attempt. It validates that ISPF detects an unsupported/conflicting multi-command set, and it provides a concrete Diagnose/Recover path.

See:

```text
docs/negative-test-command-conflict.md
```

## Maturity decision

The lab was originally planned as M2.

The final evidence supports:

```text
M3 — Resilient
```

because the executed workflow includes a real conflict, diagnosis, controlled recovery, corrected execution and post-recovery validation.

## Scope boundary

Included:

```text
R / R3 / RR
C / C2 / CC
M / M2 / MM
A / A2 / B
multiple line commands
CANCEL rollback
```

Excluded:

```text
MASK
OVERLAY
BNDS
EXCLUDE
CHANGE
UNDO
Edit Recovery
```

These remain future capabilities.

## Next capability

**Lab 11 — ISPF Edit MASK and OVERLAY**

## References

See the repository-level `references/README.md`.
