# Lab 12 — ISPF Edit BNDS, Column Shifting and Data Shifting

## Architecture metadata

```yaml
architecture:
  domain: "Operations and Service Management"
  capability: "Controlled column-bounded ISPF Edit transformation and shifting"
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

Complete Bosler Chapter 14 using deterministic column-position fixtures and evidence-driven recovery.

The lab validates:

- BNDS inspection and controlled reconfiguration;
- safe column shifting;
- destructive column shifting;
- data shifting protection;
- incomplete-shift diagnostics;
- RESET;
- block data shifting;
- profile restoration;
- independent final persistent-state validation.

## Fixture

```text
IBMUSER.ISPF.LAB(EDIT12)
```

Canonical fixture:

```text
fixtures/edit/EDIT12-baseline.txt
```

Baseline:

```text
11 records
```

## BNDS baseline and controlled bounds

`COLS` was used to make positions visible.

`BNDS` exposed the active boundary state.

A restrictive test interval was configured around the synthetic inner data fields while the `LEFT...|` and `|RIGHT...` text remained outside the active region.

## Safe column shifting

A right column shift with explicit count and a left column shift using the default count were executed.

Observed:

- bounded data moved;
- text outside the configured bounds stayed fixed;
- the mutation was cancelled;
- baseline content was restored.

## Destructive column shift

The fixture:

```text
LEFT0005|AAA BBB CCC|RIGHT05
```

was intentionally designed without free space at the configured right edge.

A right column shift caused trailing significant characters to be discarded in the Edit working state.

This destructive result was intentional and was never saved.

`CANCEL` restored the canonical line.

## Protected data shift

Command:

```text
<99
```

was issued against:

```text
LEFT0006|  JJJ KKK  |RIGHT06
```

ISPF responded:

```text
Data shifting incomplete
```

and marked the line:

```text
==ERR>
```

Significant data was preserved.

`RESET` cleared the error-display state.

## Block data shift

A two-line block was shifted right using the double-shift block form.

The two records retained order and the data outside the bounds remained intact.

## BNDS restoration

The restrictive test bounds were removed and the pre-lab/default boundary state was restored before lab closure.

## Final validation

A final independent Browse showed exactly the canonical 11 records.

```text
persistent state = BASELINE RESTORED
```

## Validation summary

| Capability | Result |
|---|---|
| BNDS baseline | PASS |
| restrictive BNDS | PASS |
| safe right column shift | PASS |
| safe left/default column shift | PASS |
| outside-bound protection | PASS |
| destructive column shift | VALIDATED |
| controlled working-state data loss | OBSERVED |
| CANCEL recovery | PASS |
| protected data shift | PASS |
| Data shifting incomplete | VALIDATED |
| `==ERR>` | VALIDATED |
| RESET | PASS |
| block data shift | PASS |
| BNDS restoration | PASS |
| final Browse baseline | PASS |

## Maturity decision

Final maturity:

```text
M3 — Resilient
```

because destructive behavior, protected incomplete behavior, recovery, profile restoration and independent post-recovery validation were all executed.

## Scope boundary

Included:

```text
BNDS
COLS
(
)
<
>
block data shift
RESET
CANCEL
```

Excluded:

```text
EXCLUDE
Edit labels
TABS
Edit primary commands
CHANGE
UNDO / Edit Recovery
```

## Next capability

**Lab 13 — ISPF Edit EXCLUDE, Edit Labels and TABS**

## References

See repository-level `references/README.md`.
