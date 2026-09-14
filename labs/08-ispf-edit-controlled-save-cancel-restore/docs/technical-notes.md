# Technical Notes — Lab 08

## Repository-owned mutation fixture

Labs 04–07 used `IBMUSER.JCL.LAB` as read-only source material.

Lab 08 changes repository policy for state-changing tests:

```text
IBMUSER.ISPF.LAB
```

is owned by the `MVS_TSO_ISPF` learning path and isolates destructive/temporary Edit activity from artifacts owned by JCL, COBOL, REXX, Assembler or other repositories.

## Baseline as a test oracle

The canonical member content is preserved under:

```text
fixtures/edit/EDIT08-baseline.txt
```

This allows the lab to define the expected final state before execution.

## SAVE versus CANCEL

The lab demonstrates two different state transitions:

```text
unsaved modification -> CANCEL -> no persistence
saved modification   -> SAVE   -> persistence
```

A second independent Browse session is used to verify both outcomes.

## AUTOSAVE observation

`PROFILE 9` showed:

```text
AUTOSAVE ON
```

For this reason the lab deliberately avoids treating PF3/END as its persistence or rollback control.

The tested operations are explicit:

```text
SAVE
CANCEL
```

## RECOVERY / UNDO observation

The profile showed:

```text
RECOVERY OFF WARN
```

and the Edit panel displayed a warning that UNDO is unavailable until the profile is changed to `RECOVERY ON`.

The lab does not alter that profile setting. This observation becomes input to a future Edit Profile / Recovery lab.

## STATS observation

The profile showed:

```text
STATS ON
```

The Edit title moved through observed member version values:

```text
01.00
01.01
01.02
```

across the persisted Edit lifecycle.

These values are retained as environment evidence. The lab does not claim that every ISPF installation will expose identical version behavior.

## M3 rationale

Architecture V2 defines resilient maturity around explicit failure/rollback/recovery and post-recovery validation.

Lab 08 satisfies that engineering objective because it executes:

1. a controlled transient modification;
2. explicit rollback with `CANCEL`;
3. independent proof that the rollback preserved the baseline;
4. a persisted modification using `SAVE`;
5. independent proof of persistence;
6. a controlled restoration;
7. independent proof that the final persistent state equals the canonical baseline.

This is stronger than documenting a hypothetical rollback procedure.
