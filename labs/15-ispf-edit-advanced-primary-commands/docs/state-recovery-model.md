# State and Recovery Model — Lab 15

## Visibility state

```text
X ALL DROP
      |
      v
display-only exclusion
```

No record is removed from the working data until DELETE is issued.

## Destructive mutation

```text
excluded records
      |
      v
DEL ALL X
      |
      v
17 -> 15 working records
      |
      v
CANCEL
      |
      v
17 canonical records
```

## Resequencing mutation

```text
03 / 01 / 04 / 02
      |
      v
SORT 6 7 A .SA .SB
      |
      v
01 / 02 / 03 / 04
      |
      v
CANCEL
      |
      v
03 / 01 / 04 / 02
```

## Recursive Edit context

```text
EDIT15 active
    |
    | EDIT EDIT15R
    v
EDIT15 suspended
EDIT15R active
    |
    | CANCEL
    v
EDIT15 resumed
```

## Final invariants

```text
EDIT15 persistent_record_count == 17
EDIT15 persistent_content == fixtures/edit/EDIT15-baseline.txt

EDIT15R persistent_record_count == 3
EDIT15R persistent_content == fixtures/edit/EDIT15R-baseline.txt
```
