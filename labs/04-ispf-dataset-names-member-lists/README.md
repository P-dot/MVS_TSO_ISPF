# Lab 04 — ISPF Data Set Names and Member List Processing

## Objective

Validate how TSO/E and ISPF identify data sets and how ISPF processes members of a partitioned data set.

The lab demonstrates:

- the active TSO prefix with `PROFILE`;
- DSLIST discovery with `=3.4`;
- data-set naming and qualifiers;
- selection of a real partitioned data set;
- member-list statistics;
- line-command selection;
- primary-command selection;
- `LOCATE`;
- `SORT`;
- `RESET`;
- member-name pattern filtering.

## Environment

- IBM z/OS 1.11 ADCD
- TSO/E
- ISPF 6.1
- 3270/TN3270 interactive session
- Lab user: `IBMUSER`

## Architectural scope

This lab validates the **interactive data-set/member layer** owned by `MVS_TSO_ISPF`.

The partitioned data set `IBMUSER.JCL.LAB` is used only as a real ISPF navigation object. The lab does not teach or validate JCL semantics; those remain the responsibility of `JCL_LABS`.

```text
MVS_TSO_ISPF
      |
      +--> data-set discovery
      +--> member-list processing
      |
      +--------------------> JCL_LABS
                               |
                               +--> JCL semantics / JES2 workflow
```

## 1. Confirm the TSO prefix

From ISPF option 6, the TSO command:

```text
PROFILE
```

returned a profile containing:

```text
PREFIX(IBMUSER)
```

This provides the TSO naming context used by the lab.

Evidence:

- `01-profile-prefix-ibmuser.png`

## 2. Enter DSLIST and list the IBMUSER level

The direct ISPF route:

```text
=3.4
```

opened the Data Set List Utility.

The field:

```text
Dsname Level . . . IBMUSER
```

was used to list matching cataloged data sets.

Observed result:

```text
DSLIST - Data Sets Matching IBMUSER
Row 1 of 142
```

Evidence:

- `02-dslist-dsname-level-ibmuser.png`
- `03-dslist-142-data-sets.png`

## 3. Data-set naming

The data set selected for the member-list work was:

```text
IBMUSER.JCL.LAB
```

Its qualifiers can be read as:

```text
IBMUSER . JCL . LAB
   |       |     |
   |       |     +-- low-level qualifier
   |       +-------- intermediate qualifier
   +---------------- high-level qualifier
```

A member is written using parentheses:

```text
IBMUSER.JCL.LAB(CALLPRC2)
```

This lab uses the naming structure as an ISPF/TSO concept. The semantic meaning of JCL members is outside the lab scope.

## 4. Open a member list safely

In DSLIST, the line command:

```text
B
```

was entered next to:

```text
IBMUSER.JCL.LAB
```

Browse was intentionally used instead of Edit to avoid modifying the PDS while studying member-list processing.

Evidence:

- `04-browse-select-ibmuser-jcl-lab.png`

ISPF then displayed a member list with:

```text
54 members
```

and columns including:

```text
Name
Prompt
Size
Created
Changed
ID
```

Evidence:

- `05-member-list-54-members-top.png`
- `06-member-list-54-members-end.png`

## 5. Select a member with a line command

The line command:

```text
S
```

was placed next to:

```text
CALLPRC2
```

The selected member opened in Browse as:

```text
IBMUSER.JCL.LAB(CALLPRC2)
```

This demonstrates a **line command**, which acts on the specific row where it is entered.

Evidence:

- `07-line-command-s-callprc2.png`
- `08-browse-callprc2.png`

## 6. Select a member with a primary command

From the member list, the primary command:

```text
SELECT RACFDSMN
```

selected a member by name without requiring that row to be used as a line-command target.

The member opened in Browse as:

```text
IBMUSER.JCL.LAB(RACFDSMN)
```

Evidence:

- `09-primary-command-select-racfdsnm.png`
- `10-browse-racfdsnm.png`

This establishes the distinction:

```text
line command:
S  CALLPRC2

primary command:
SELECT RACFDSMN
```

## 7. LOCATE by prefix

The command:

```text
L RACF
```

repositioned the member list to the group of members whose names begin with `RACF`.

Evidence:

- `11-locate-racf-command.png`
- `12-locate-racf-result.png`

This is more efficient than paging repeatedly through a larger PDS.

## 8. SORT by member statistics

The lab tested three sort keys.

### Changed

```text
SORT CHANGED
```

The result placed recently changed members toward the top.

Evidence:

- `13-sort-changed-command.png`
- `14-sort-changed-result.png`

### Size

```text
SORT SIZE
```

The result ordered the list by member size, with larger values at the top.

Evidence:

- `15-sort-size-command.png`
- `16-sort-size-result.png`

### Name

```text
SORT NAME
```

The result restored name-oriented ordering.

Evidence:

- `17-sort-name-command.png`
- `18-sort-name-result.png`

## 9. Clear pending line commands with RESET

Two pending line commands were entered:

```text
S  CALLPRC2
S  CALLPROC
```

At the same time the primary command field contained:

```text
RESET
```

After execution, the pending `S` commands were cleared and no member was opened.

Evidence:

- `19-reset-pending-line-commands.png`
- `20-reset-result-cleared.png`

`RESET` here is a **member-list control operation**. It is not an undo of PDS data changes.

## 10. Filter the member list with a pattern

From the View Entry Panel, the data-set/member specification:

```text
IBMUSER.JCL.LAB(L1*)
```

was entered.

Evidence:

- `21-view-member-pattern-l1-star.png`

The resulting member list contained only matching names beginning with `L1`.

Observed result:

```text
22 matching members
```

Evidence:

- `22-member-pattern-l1-star-result.png`

This demonstrates pattern-based member selection:

```text
IBMUSER.JCL.LAB
        |
        +--> 54 members

IBMUSER.JCL.LAB(L1*)
        |
        +--> 22 matching members
```

## Verified operations

| Operation | Verified result |
|---|---|
| `PROFILE` | TSO profile showed `PREFIX(IBMUSER)` |
| `=3.4` | Opened ISPF Data Set List Utility |
| `Dsname Level = IBMUSER` | Listed 142 matching data sets |
| `B` on `IBMUSER.JCL.LAB` | Opened a 54-member PDS list in Browse |
| line `S` | Selected the member on that row |
| `SELECT member` | Selected a named member using a primary command |
| `L RACF` | Repositioned list to the RACF-prefixed area |
| `SORT CHANGED` | Ordered by change information |
| `SORT SIZE` | Ordered by member size |
| `SORT NAME` | Restored name ordering |
| `RESET` | Cleared pending member-list line commands |
| `L1*` | Filtered the list to 22 matching members |

## Result

**Lab status: SUCCESS**

The lab closes the transition from basic ISPF navigation to real z/OS data-set/member work:

```text
TSO/E
  |
  v
ISPF
  |
  v
DSLIST
  |
  v
cataloged data sets
  |
  v
partitioned data set
  |
  v
member list
  |
  +--> select
  +--> locate
  +--> sort
  +--> reset
  +--> pattern filter
```

The next logical layer is to study **Browse behavior itself**, followed by Edit and the wider ISPF utilities.

## Publication security

The selected evidence begins inside TSO/ISPF and excludes password/logon credential screens.

See `docs/security-review.md`.

## References

See the repository-level `references/README.md`.
