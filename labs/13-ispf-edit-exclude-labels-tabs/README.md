# Lab 13 — ISPF Edit EXCLUDE, Labels and TABS Display State

## Architecture metadata

```yaml
architecture:
  domain: "Operations and Service Management"
  capability: "Selective ISPF Edit visibility, session-scoped positioning and special-line state inspection"
  lifecycle:
    - Baseline
    - Operate
    - Observe
  maturity: "M2 — Operational"
  integration_level: "I0 — Standalone"
```

## Objective

Validate Chapter 15 Edit line-command behavior as one coherent operational capability:

- selectively hide records without deleting them;
- partially redisplay an excluded set;
- use structural SHOW behavior;
- create and locate session labels;
- use built-in positional labels;
- inspect and clear the TABS special-line state;
- prove the persistent member remains unchanged.

## Fixture

```text
IBMUSER.ISPF.LAB(EDIT13)
```

Canonical fixture:

```text
fixtures/edit/EDIT13-baseline.txt
```

Baseline:

```text
18 records
```

## Capability 1 — Selective visibility

Validated:

```text
X
X3
XX / XX
```

Observed special-line states included:

```text
1 Line(s) not Displayed
3 Line(s) not Displayed
5 Line(s) not Displayed
```

The member data itself was not deleted.

## Capability 2 — Partial redisplay

Against the `X3` block:

```text
F
```

redisplayed the first excluded record.

Then:

```text
L
```

redisplayed the last record of the remaining excluded group.

This left exactly one line excluded until `RESET` restored the complete display.

## Capability 3 — SHOW and indentation

A five-record hierarchy was excluded:

```text
ROOT
  CHILD-A
    GRANDCHILD-A
  CHILD-B
    GRANDCHILD-B
```

`S2` redisplayed:

```text
ROOT
  CHILD-A
```

and left three records excluded.

This validates indentation-aware SHOW selection in the tested ISPF 6.1 environment.

## Capability 4 — Edit labels

User-defined labels:

```text
.START
.MID
.END
```

were created in the line-command area.

Validated positioning:

```text
L .MID
L .ZLAST
L .ZFIRST
```

`RESET LABEL` removed the user-defined labels.

The labels were session state, not dataset content.

## Capability 5 — TABS display state

The `TABS` line command displayed:

```text
=TABS>
```

No advanced tab configuration was changed.

`RESET SPECIAL` removed the special line.

## State model

Lab 13 keeps four state domains distinct:

```text
persistent dataset data
display exclusion state
session label/position state
special-line display state
```

## Final validation

A final Browse displayed exactly the 18 canonical records.

```text
persistent state = BASELINE UNCHANGED
```

## Validation summary

| Capability | Result |
|---|---|
| baseline | PASS |
| `X` | PASS |
| `X3` | PASS |
| `F` | PASS |
| `L` | PASS |
| `XX/XX` | PASS |
| `S2` | PASS |
| indentation behavior | OBSERVED |
| custom labels | PASS |
| `L .MID` | PASS |
| `.ZLAST` | PASS |
| `.ZFIRST` | PASS |
| `RESET LABEL` | PASS |
| `=TABS>` | PASS |
| `RESET SPECIAL` | PASS |
| final 18-record Browse | PASS |

## Maturity decision

Final maturity:

```text
M2 — Operational
```

The lab demonstrates reliable operation and observation. It intentionally does not manufacture a failure merely to justify M3.

## Architecture V2 downstream relationship

```text
MVS / TSO / ISPF
      |
      v
REXX
      |
      v
Production Track 08
Operations Automation
```

This lab validates the interactive capability only. Cross-repository automation remains a later integration responsibility.

## Next capability

**Bosler Chapter 16 — Edit Primary Commands**

```text
HEX
FIND
LOCATE
RESET
SUBMIT
```

## References

See repository-level `references/README.md`.


---
### Continue learning

**Previous:** [12-ispf-edit-bnds-column-data-shifting](../12-ispf-edit-bnds-column-data-shifting/)  
**Course:** [Course home](../../README.md)  
**Next:** [14-ispf-edit-primary-commands](../14-ispf-edit-primary-commands/)  
**Academy:** [z/OS Engineering Academy](https://github.com/P-dot/P-dot/blob/main/docs/ACADEMY.md) · [Curriculum](https://github.com/P-dot/P-dot/blob/main/docs/CURRICULUM.md)
