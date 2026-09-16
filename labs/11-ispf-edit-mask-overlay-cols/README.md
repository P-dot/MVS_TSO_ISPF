# Lab 11 — ISPF Edit MASK and OVERLAY: Templated Input, Controlled Data Merge and Column Indicators

## Architecture metadata

```yaml
architecture:
  domain: "Operations and Service Management"
  capability: "Controlled ISPF Edit templated insertion, overlay merge and column-position inspection"
  lifecycle:
    - Baseline
    - Configure
    - Operate
    - Observe
    - Diagnose
    - Recover
  maturity: "M3 — Resilient"
  integration_level: "I0 — Standalone"
```

## Objective

Complete Bosler Chapter 13 by validating MASK, OVERLAY and Edit column indicators with deterministic evidence, state restoration and negative/protective behavior analysis.

## Fixture

```text
IBMUSER.ISPF.LAB(EDIT11)
```

Canonical baseline:

```text
ISPF-LAB11-BASELINE
MASK-ANCHOR
KEEP-MASK
OVL-COPY-SOURCE
OVL-COPY-TARGET
OVL-BLOCK-SOURCE-A
OVL-BLOCK-SOURCE-B
OVL-BLOCK-TARGET-A
OVL-BLOCK-TARGET-B
OVL-MOVE-SOURCE
OVL-MOVE-TARGET
ISPF-LAB11-END
```

Record count:

```text
12
```

## MASK validation

The pre-lab mask profile was blank.

A controlled template was configured and used by `I3`.

Only populated input lines survived; an unused masked insert line disappeared.

The `=MASK>` display was hidden, while subsequent INSERT still inherited the stored template.

The mask was redisplayed and later restored to blank.

Dataset mutations were cancelled and independent Browse returned to the 12-record baseline.

## COPY + OVERLAY

Temporary source:

```text
OVL-COPY-SOURCE-ADD
```

Using:

```text
C
O
```

produced:

```text
OVL-COPY-TARGET-ADD
```

while the source remained.

Record count did not change.

## Block OVERLAY

Temporary sources:

```text
OVL-BLOCK-SOURCE-A-X
OVL-BLOCK-SOURCE-B-Y
```

A block source and block overlay destination produced:

```text
OVL-BLOCK-TARGET-A-X
OVL-BLOCK-TARGET-B-Y
```

Source order was preserved.

A transient `Command conflict` was observed during setup, documented without inventing a root cause.

## Protected MOVE + OVERLAY

`M + O` against the MOVE source/target pair produced:

```text
Line not deleted
```

The source remained present because not all source data could be placed on the target.

This is retained as a protective negative test.

## COLS validation

`COLS` was entered as a line command.

One `=COLS>` indicator was displayed, followed by a second independent indicator.

Both coexisted on screen.

A `D` line command removed one indicator without deleting any real record.

`CANCEL` removed the temporary working-state displays, and final Browse showed exactly the canonical 12 records.

## Validation summary

| Capability | Result |
|---|---|
| MASK profile baseline | PASS |
| MASK templated INSERT | PASS |
| Hidden MASK remains effective | PASS |
| MASK profile restore | PASS |
| C + O | PASS |
| CC/OO block overlay | PASS |
| MOVE + O protection | PASS |
| `Line not deleted` | VALIDATED |
| COLS | PASS |
| multiple COLS | PASS |
| special-line deletion safety | PASS |
| final rollback | PASS |
| final persistent state | 12-record baseline |

## Maturity decision

Final maturity:

```text
M3 — Resilient
```

because the evidence includes profile-state restoration, repeated rollback, a real protected MOVE/OVERLAY condition, conflict diagnosis and independent post-recovery verification.

## Scope boundary

Included:

```text
MASK
OVERLAY
O / OO
COLS
CANCEL rollback
```

Excluded:

```text
BNDS
column shift
data shift
EXCLUDE
CHANGE
UNDO
Edit Recovery
```

## Next capability

**Lab 12 — ISPF Edit BNDS and Column/Data Shifting**

## References

See repository-level `references/README.md`.
