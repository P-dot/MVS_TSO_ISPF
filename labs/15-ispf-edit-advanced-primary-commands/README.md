# Lab 15 — ISPF Edit Advanced Primary Commands: EXCLUDE, DELETE, SORT and Recursive Edit

## Architecture metadata

```yaml
architecture:
  domain: "Operations and Service Management"
  capability: "Content-driven selection, scoped mutation, resequencing and nested Edit context"
  lifecycle:
    - Baseline
    - Configure
    - Operate
    - Observe
    - Recover
  maturity: "M3 — Resilient"
  integration_level: "I0 — Standalone"
```

## Objective

Validate Bosler Chapter 17 as a coherent advanced Edit capability:

- drive EXCLUDE by data content;
- drive EXCLUDE by label range;
- convert excluded state into destructive DELETE;
- recover destructive working-state changes;
- resequence a controlled range with SORT;
- recover original sequence;
- invoke and return from recursive Edit.

## Fixtures

Primary:

```text
IBMUSER.ISPF.LAB(EDIT15)
```

Canonical:

```text
fixtures/edit/EDIT15-baseline.txt
```

Records:

```text
17
```

Recursive child:

```text
IBMUSER.ISPF.LAB(EDIT15R)
```

Canonical:

```text
fixtures/edit/EDIT15R-baseline.txt
```

Records:

```text
3
```

## Content-driven EXCLUDE

```text
X ALL DROP
```

excluded exactly:

```text
EXC-DROP-01 ALPHA
EXC-DROP-02 BETA
```

`RESET EXCLUDED` restored the display.

## Label-range EXCLUDE

Labels:

```text
.XA  LABEL-RANGE-START
.XB  LABEL-RANGE-END
```

The tested environment required:

```text
EXCLUDE ALL .XA .XB
```

This excluded the complete four-record range.

A shorter source-style attempt:

```text
EXCLUDE .XA .XB
```

produced:

```text
Put string in quotes
```

That environment-specific behavior is preserved in the evidence.

## DELETE and recovery

The two DROP records were excluded again and:

```text
DEL ALL X
```

produced:

```text
2 lines deleted
```

The working-state count changed:

```text
17 -> 15
```

No SAVE was issued.

`CANCEL` restored the canonical 17-record member.

## SORT and recovery

Controlled range:

```text
SORT-03|CHARLIE
SORT-01|ALPHA
SORT-04|DELTA
SORT-02|BRAVO
```

Labels:

```text
.SA
.SB
```

Command:

```text
SORT 6 7 A .SA .SB
```

Result:

```text
SORT-01|ALPHA
SORT-02|BRAVO
SORT-03|CHARLIE
SORT-04|DELTA
```

`CANCEL` restored the original canonical order.

## Recursive Edit

From `EDIT15`:

```text
EDIT EDIT15R
```

activated:

```text
IBMUSER.ISPF.LAB(EDIT15R)
```

with the expected three records.

`CANCEL` in the child session returned directly to the parent:

```text
IBMUSER.ISPF.LAB(EDIT15)
```

## Final classification

```text
VALIDATED
M3 — Resilient
I0 — Standalone
```

M3 is supported by actual destructive and resequencing working-state mutations followed by explicit rollback and verified context recovery.

## Next capability

**Bosler Chapter 18 — CHANGE Command**
