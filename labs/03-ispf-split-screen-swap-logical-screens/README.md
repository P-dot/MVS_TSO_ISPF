# Lab 03 — ISPF Split Screen, SWAP and Logical Screens

## Objective

Validate how ISPF maintains more than one logical screen inside the same TSO/E and ISPF session, and demonstrate how the user can:

- create another logical screen with `SPLIT` / `F2`;
- move between logical screens with `SWAP` / `F9`;
- preserve independent ISPF panel state;
- inspect active logical screens with `SWAP LIST`;
- terminate one logical screen with `END` / `F3`;
- confirm that only one logical screen remains.

## Environment

- IBM z/OS 1.11 ADCD
- TSO/E
- ISPF 6.1
- 3270 session
- Lab user: `IBMUSER`

## Scope

This lab remains inside the interactive TSO/E and ISPF foundation owned by this repository.

It does not implement REXX automation, JCL logic, scheduler behavior, RACF administration or Communications Server configuration. Those responsibilities remain in their specialized repositories.

## Concepts

### Logical screen

An ISPF logical screen is an independent ISPF work context maintained inside the same ISPF session.

The lab validated the following model:

```text
TSO/E session
      |
      v
     ISPF
      |
      +-- Logical Screen 1
      |       |
      |       +-- Utilities
      |
      +-- Logical Screen 2
              |
              +-- Edit
```

These are not separate TSO logons, users or TN3270 connections.

### SPLIT / F2

`F2` was used to invoke the ISPF split function and create an additional logical-screen context.

In this terminal layout the evidence shows each active logical screen full-screen when selected rather than preserving a permanently visible two-pane layout. The logical-screen count and identity were therefore validated with the ISPF task list instead of relying only on the visual split.

### SWAP / F9

`F9` was used to move between the active logical screens.

Different ISPF functions were left active:

```text
Logical Screen 1 -> Utilities
Logical Screen 2 -> Edit
```

Returning to each screen preserved its panel state.

### SWAP LIST

The command:

```text
SWAP LIST
```

displayed the **ISPF Task List**.

The task list showed two active ISPF logical sessions:

```text
Name   Panelid    Applid   Session Type
UTIL   ISRUTIL    ISR      3270
EDIT   ISREDM01   ISR      3270
```

This was the strongest validation that ISPF was maintaining two logical contexts and not merely navigating between ordinary panels.

### END / F3

One logical-screen context was ended.

A final `SWAP LIST` showed a single remaining active logical session, validating the logical-screen lifecycle.

## Executed flow

```text
Primary Option Menu
        |
        | F2 / SPLIT
        v
additional logical screen
        |
        +----> Edit
        |
       F9 / SWAP
        |
        +----> Utilities
        |
       F9 / SWAP
        |
        v
previous panel state preserved
        |
        | SWAP LIST
        v
ISPF Task List: 2 logical screens
        |
        | RETURN / F3 as required
        v
one logical screen ended
        |
        | SWAP LIST
        v
ISPF Task List: 1 logical screen
```

## Evidence

| Evidence | What it demonstrates |
|---|---|
| `01-primary-before-split.png` | Initial ISPF context |
| `02-second-logical-screen-created.png` | A second logical-screen context exists (`Screen 2`) |
| `03-edit-on-logical-screen.png` | Edit assigned to one logical screen |
| `04-utilities-on-other-logical-screen.png` | Utilities assigned to the other logical screen |
| `05-edit-state-preserved-after-swap.png` | Edit context preserved after switching |
| `06-swap-list-command.png` | `SWAP LIST` invocation |
| `07-task-list-two-logical-screens.png` | Two active logical screens listed by ISPF |
| `08-logical-screen-1-primary.png` | Logical Screen 1 active |
| `09-logical-screen-2-primary.png` | Logical Screen 2 active |
| `10-task-list-single-logical-screen.png` | Final validation: one logical screen remains |

## Result

**Lab status: SUCCESS**

The lab validated:

```text
F2 / SPLIT
      |
      v
multiple ISPF logical screens
      |
      +-- independent panel state
      |
F9 / SWAP
      |
      v
switch active context
      |
SWAP LIST
      |
      v
2 active logical screens
      |
F3 / END
      |
      v
1 logical screen remains
```

The practical value is that a user can keep one ISPF task available while consulting or working in another context without destroying the first task's state.

This provides a stronger operator foundation for later dataset, editor, utility and REXX/ISPF automation work.

## Publication security

The selected screenshots begin inside ISPF and do not include the TSO logon/password sequence.

See `docs/security-review.md`.

## References

See the repository-level `references/README.md`.
