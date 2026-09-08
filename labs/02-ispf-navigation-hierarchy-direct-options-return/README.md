# Lab 02 — ISPF Navigation, Hierarchy, Direct Options and RETURN

## Objective

Demonstrate how ISPF navigation works in a real z/OS 1.11 environment by comparing:

- normal hierarchical navigation,
- direct option entry,
- the ISPF jump function,
- `F3` / `END`,
- and `RETURN`.

The lab verifies the behavior directly in ISPF 6.1 instead of treating the navigation model as theory only.

## Environment

- IBM z/OS 1.11 ADCD
- TSO/E
- ISPF 6.1
- User used for the lab: `IBMUSER`

## Concepts

ISPF is organized as a hierarchy of panels and functions. A selection on one menu can lead to another menu, which can contain further suboptions.

The route verified in this lab is:

```text
ISPF Primary Option Menu
        |
        +-- 3 Utilities
              |
              +-- 4 Dslist
```

The same final function can be reached in different ways.

### Hierarchical navigation

```text
3
|
v
Utility Selection Panel
|
4
|
v
Data Set List Utility
```

### Direct option entry

From the Primary Option Menu:

```text
3.4
```

This enters the Data Set List Utility directly without stopping at the intermediate Utilities panel.

### Jump function

From another ISPF function, in this lab the Edit Entry Panel:

```text
=3.4
```

The leading `=` requests a jump to the specified ISPF path.

### F3 / END

`F3` is normally mapped to `END`.

In this lab:

```text
Data Set List Utility
        |
       F3
        |
        v
Utility Selection Panel
```

It ended the current function and returned one level in the navigation path.

### RETURN

From the Data Set List Utility:

```text
RETURN
```

returned directly to the ISPF Primary Option Menu.

This is different from repeatedly using `F3` to traverse intermediate panels.

## Executed flow

### 1. Start from the ISPF Primary Option Menu

The Primary Option Menu was used as the starting point for the navigation tests.

Evidence:

- `01-primary-option-menu.png`

### 2. Select Utilities with option 3

Command:

```text
3
```

Observed result:

```text
Utility Selection Panel
```

Evidence:

- `02-select-utilities-option-3.png`
- `03-utility-selection-panel.png`

### 3. Select Dslist with option 4

Command:

```text
4
```

Observed result:

```text
Data Set List Utility
```

Evidence:

- `04-select-dslist-option-4.png`
- `05-dslist-via-hierarchy.png`

This verified:

```text
3 -> 4
```

### 4. Use direct option entry

From the Primary Option Menu:

```text
3.4
```

Observed result:

```text
Data Set List Utility
```

without stopping at the Utilities panel.

Evidence:

- `06-primary-menu-direct-3-4.png`
- `07-dslist-via-direct-option.png`

### 5. Use the ISPF jump function

The Edit Entry Panel was opened, and from that different ISPF function the following command was entered:

```text
=3.4
```

Observed result:

```text
Data Set List Utility
```

Evidence:

- `08-edit-entry-panel.png`
- `09-jump-command-equals-3-4.png`
- `10-dslist-after-jump.png`

This verified that the jump function can move directly to another ISPF path without manually backing out through the previous panels.

### 6. Use RETURN

From the Data Set List Utility:

```text
RETURN
```

Observed result:

```text
ISPF Primary Option Menu
```

Evidence:

- `11-return-command-from-dslist.png`
- `12-primary-menu-after-return.png`

## Verified command behavior

| Entry | Verified behavior |
|---|---|
| `3` | Entered Utilities from the Primary Option Menu |
| `4` | Entered Dslist from the Utility Selection Panel |
| `3.4` | Entered Dslist directly from the Primary Option Menu |
| `=3.4` | Jumped to Dslist from the Edit Entry Panel |
| `F3` / `END` | Returned from Dslist to the previous Utilities panel |
| `RETURN` | Returned from Dslist directly to the Primary Option Menu |

## Result

**Lab status: SUCCESS**

The lab demonstrated that ISPF navigation is not limited to moving through menus one panel at a time. Direct paths and the jump function reduce the number of panels required, while `F3`/`END` and `RETURN` provide different ways to leave the current function.

The practical difference is:

```text
Hierarchical:
3 -> 4

Direct:
3.4

Jump from another function:
=3.4

Back one level:
F3 / END

Return to Primary Option Menu:
RETURN
```

These navigation techniques form an important base for more efficient daily work in ISPF and for later automation-oriented labs.

## Evidence

All selected evidence is stored in:

```text
evidence/
```

Only screenshots needed to prove the Lab 02 objectives are included. The repeated TSO logon sequence from Lab 01 was intentionally omitted.

## Security

The selected Lab 02 screenshots were reviewed before packaging.

- No password screens are included.
- No ADCD default credential table is included.
- No IP addresses are shown.
- No MAC addresses are shown.
- No host network adapter information is included.

See:

```text
docs/security-review.md
```

## References

- Kurt Bosler, *MVS TSO/ISPF: A Guide for Users and Developers*, Chapter 4, Accessing ISPF.
- Franz Lanz, *IBM z/OS ISPF Smart Practices, Volume 1: User's Guide*, especially the sections covering ISPF panels and the Primary Option Menu.
- IBM Redbooks, *Introduction to the New Mainframe: z/OS Basics*, SG24-6366-00.
- IBM Redbooks, *z/OS Version 1 Release 11 Implementation*, SG24-7729-00, used as the release-specific z/OS context for this project.
