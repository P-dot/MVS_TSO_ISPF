# Lab 09 — ISPF Edit Line Commands: Controlled Record Insertion and Deletion

## Objective

Validate basic ISPF Edit record insertion and deletion using deterministic record-count transitions, explicit rollback, incomplete-block recovery, and independent final-state verification.

## Architecture V2

```text
Domain: Operations and Service Management
Capability: Controlled ISPF Edit record insertion and deletion
Lifecycle: Baseline / Configure / Operate / Observe / Recover
Maturity: M3 — Resilient
Integration: I0 — Standalone
Validation: VALIDATED
```

## Fixture

`IBMUSER.ISPF.LAB(EDIT09)`

Canonical baseline: 13 records. See `fixtures/edit/EDIT09-baseline.txt`.

## INSERT validation

`I` produced one input record: 13 -> 14.

`I3` produced three additional input records: 14 -> 17.

`CANCEL` discarded the insertion sequence. Independent Browse returned to the canonical 13-record baseline.

## DELETE validation

`D` removed `DEL-SINGLE`: 13 -> 12.

`D3` removed `DEL-MULTI-A/B/C`: 12 -> 9.

A single `DD` generated `Block command incomplete`. `RESET` cleared the pending block command with no data deletion.

A complete `DD` / `DD` pair removed `DEL-BLOCK-A/B/C`: 9 -> 6.

The six remaining working records were:

```text
ISPF-LAB09-BASELINE
KEEP-01
KEEP-02
KEEP-03
KEEP-04
ISPF-LAB09-END
```

`CANCEL` discarded the destructive sequence. Independent Browse verified all 13 original records.

## Observed exception

`Invalid command name` appeared transiently during execution. The exact invalid input is not visible in the captured evidence, so no unsupported root cause is claimed.

## Result

```text
INSERT: PASS
DELETE: PASS
Pending block handling: PASS
RESET recovery: PASS
Rollback: PASS
Final persistent record count: 13
Final persistent state: BASELINE RESTORED
```

## Maturity

The lab was planned as M2. The executed evidence supports **M3 — Resilient** because it includes rollback, incomplete-block recovery, and independent post-recovery validation.

## Scope boundary

Included: `I`, `I3`, `D`, `D3`, `DD/DD`, `RESET`, `CANCEL`.

Excluded: `R/Rn/RR`, `C/Cn/CC`, `M/Mn/MM`, `A`, `B`, MASK, OVERLAY, BNDS, EXCLUDE, CHANGE.

## Next capability

**Lab 10 — ISPF Edit Line Commands: Repeat, Copy, Move, Before and After**
