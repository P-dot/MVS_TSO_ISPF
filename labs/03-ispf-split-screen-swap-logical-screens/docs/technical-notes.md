# Technical Notes — Lab 03

## Observed behavior

The lab used the system's configured PF-key mappings:

```text
F2 = Split
F3 = Exit / END
F9 = Swap
```

The Primary Option Menu also displayed the active logical-screen number in the `Screen` field.

## Logical-screen state

Different functions were left active on different logical screens:

- `UTIL` with panel `ISRUTIL`;
- `EDIT` with panel `ISREDM01`.

`SWAP LIST` exposed these as separate active ISPF logical sessions with `Applid ISR` and session type `3270`.

## Why SWAP LIST matters

A visual screen change alone could be confused with normal panel navigation.

The ISPF Task List provides stronger evidence because it explicitly enumerates the active logical-screen contexts.

## Terminal-layout observation

The lab evidence does not show two persistent half-screen panes at the same time. Instead, each selected logical screen occupied the terminal display while the `Screen` field and `SWAP LIST` identified the active contexts.

The lab therefore documents the behavior actually observed on this z/OS 1.11 / ISPF 6.1 environment rather than assuming a particular split-screen visual layout.

## Lifecycle validation

Before ending one context:

```text
UTIL
EDIT
```

were both present in the ISPF Task List.

After ending one context, the final Task List contained one remaining logical session.

This closes the validation loop:

```text
create -> use -> swap -> enumerate -> end -> enumerate again
```

## Architectural relevance

This lab remains in the `MVS_TSO_ISPF` repository because logical-screen operation is part of the interactive ISPF foundation.

Later repositories can consume this foundation:

```text
MVS_TSO_ISPF
     |
     +--> JCL_LABS
     |
     +--> Rexx
              |
              v
        ISPF automation
```

The domain-specific logic stays in those repositories.
