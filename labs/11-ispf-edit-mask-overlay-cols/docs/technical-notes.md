# Technical Notes — Lab 11

## MASK belongs to the Edit Profile

The mask line is not a normal dataset record. Its value can remain active even when the `=MASK>` display line is hidden.

Lab 11 therefore treats mask configuration as profile state distinct from dataset working state.

## Templated INSERT

A configured mask initialized new insert lines.

A requested masked insert line that received no user-entered data did not persist as a new record, while populated rows remained in the working state.

## OVERLAY semantics

OVERLAY acts as a merge destination for COPY or MOVE source data.

Existing meaningful target data remained, while source data occupied available positions.

## Protected MOVE/OVERLAY

The environment displayed:

```text
Line not deleted
```

when not all source data could be placed on the target.

The source record remained. This is retained as positive evidence of data-loss protection.

## Command conflict

A transient `Command conflict` was observed while setting up block overlay.

The evidence confirms the conflict but does not prove a deeper internal cause. The repository does not invent one.

## COLS

`COLS` was validated as an Edit line command.

Two column-indicator special lines were displayed simultaneously.

Deleting one special `=COLS>` line did not delete dataset data.

## M3 rationale

The lab includes:

- profile state baseline and restoration;
- data rollback;
- protected move/overlay behavior;
- conflict observation;
- multiple independent post-recovery validations.

The final M3 classification is evidence-driven.
