# Technical Notes — Lab 04

## Data-set naming

The lab uses a three-qualifier data-set name:

```text
IBMUSER.JCL.LAB
```

The leftmost qualifier is the high-level qualifier (HLQ). The rightmost qualifier is the low-level qualifier (LLQ).

A PDS member is represented with parentheses:

```text
IBMUSER.JCL.LAB(CALLPRC2)
```

## TSO prefix

`PROFILE` returned:

```text
PREFIX(IBMUSER)
```

This establishes the TSO naming context for the user session.

The lab does not infer that every ISPF panel handles prefixing identically. Instead, it validates the exact behavior of DSLIST with `Dsname Level = IBMUSER`.

## DSLIST result

The Data Set List Utility returned:

```text
142
```

matching data sets for the `IBMUSER` level.

The lab intentionally uses the returned catalog view instead of assuming which data sets exist.

## Selected PDS

`IBMUSER.JCL.LAB` was selected because it is:

- under the lab user's HLQ;
- partitioned;
- populated with multiple members;
- safe for Browse-oriented member-list experiments.

The fact that the members contain JCL is not part of this lab's technical scope.

## Member-list statistics

The observed member list exposed:

- member name;
- prompt/status;
- size;
- creation date;
- changed timestamp;
- user ID.

These columns allow member lists to function not only as selectors but also as an operational inventory.

## Line command versus primary command

A line command is attached to a particular row:

```text
S  CALLPRC2
```

A primary command identifies its target in the command field:

```text
SELECT RACFDSMN
```

The lab validates both interaction models.

## LOCATE

`L RACF` repositioned the list to members sharing the `RACF` prefix.

This is a navigation operation; it does not filter the member list.

## SORT

The lab validated:

```text
SORT CHANGED
SORT SIZE
SORT NAME
```

Sorting changes presentation order, not member contents.

## RESET

`RESET` cleared pending member-list line commands.

It did not restore data, reverse edits or change PDS contents.

## Member-name pattern

The View specification:

```text
IBMUSER.JCL.LAB(L1*)
```

produced a filtered member list containing 22 members matching the `L1*` pattern.

This is different from `LOCATE`:

```text
LOCATE -> reposition inside the existing list
pattern -> construct a matching member list
```

## Architectural relevance

Lab 04 validates the interactive prerequisite for several downstream repositories:

```text
MVS_TSO_ISPF
      |
      +--> data sets / members
      |
      +--> JCL_LABS
      +--> COBOL
      +--> PL-I
      +--> z_Assembly
      +--> Rexx
```

The relationship is foundational: those repositories consume data-set/member interaction, but retain ownership of their own language, batch or automation semantics.
