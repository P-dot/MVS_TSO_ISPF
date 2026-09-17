# Technical Notes — Lab 12

## BNDS

BNDS establishes the columns within which several Edit operations act.

The lab first captures the active/default state, then uses restrictive test bounds for deterministic shifting experiments.

The restrictive settings are restored before closure.

## Column shift versus data shift

Column shift preserves internal spacing but can discard characters that cross a configured bound.

Data shift treats meaningful data differently: when the requested shift cannot be completed safely, ISPF stops at the boundary rather than destroying significant data.

Lab 12 demonstrates both behaviors on purpose.

## Destructive test

`LEFT0005|AAA BBB CCC|RIGHT05` was selected because its bounded region contains no spare room at the right side.

A right column shift therefore caused visible working-state truncation.

The transaction was not saved; `CANCEL` restored the canonical source record.

## Data shifting incomplete

`<99` deliberately requested a shift larger than the available free space.

Observed:

```text
Data shifting incomplete
==ERR>
```

Significant data remained.

`RESET` cleared the error-display state.

## Block shift

The `>>2` block form was validated on two records, showing that a contiguous block can be shifted while retaining line order.

## M3 rationale

The maturity classification is evidence-driven:

- destructive working-state behavior was demonstrated;
- rollback was executed;
- protected incomplete shifting was demonstrated;
- error state was recovered with RESET;
- BNDS profile state was restored;
- a final independent Browse proved the persistent fixture returned to baseline.
