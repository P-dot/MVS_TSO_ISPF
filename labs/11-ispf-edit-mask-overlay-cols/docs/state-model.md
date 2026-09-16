# State Model — Lab 11

## Two independent state domains

```text
DATA STATE
IBMUSER.ISPF.LAB(EDIT11)

PROFILE STATE
=MASK> value
```

Both must be restored before lab closure.

## MASK path

```text
profile MASK blank
      |
configure template
      |
I3 / masked data entry
      |
hide / redisplay
      |
restore MASK blank
      |
CANCEL
      |
12-record baseline
```

## OVERLAY path

```text
COPY + OVERLAY
source retained
target merged
record count unchanged
      |
CANCEL
      |
12-record baseline
```

Protected MOVE path:

```text
MOVE + OVERLAY
      |
target cannot accept all source data
      |
Line not deleted
      |
source preserved
      |
CANCEL
      |
12-record baseline
```

## COLS path

```text
COLS
  -> one special indicator
COLS
  -> two indicators
D on =COLS>
  -> one indicator removed
CANCEL
  -> special lines disappear
BROWSE
  -> 12 real records only
```

## Final invariant

```text
persistent_record_count == 12
persistent_content == fixtures/edit/EDIT11-baseline.txt
MASK profile == pre-lab blank state
```
