# MVS TSO/ISPF Ecosystem Integration

## Validated capability progression

```text
Lab 08  controlled Edit / SAVE / CANCEL / restore
Lab 09  INSERT / DELETE
Lab 10  Repeat / Copy / Move / A / B
Lab 11  MASK / OVERLAY / COLS
Lab 12  BNDS / column shifting / data shifting
Lab 13  EXCLUDE / labels / TABS display state
Lab 14  HEX / FIND / LOCATE / selective RESET
Lab 15  primary EXCLUDE / DELETE / SORT / Recursive Edit
```

## Lab 15 ownership

Repository-owned capability:

```text
content-driven visibility
label-range scoping
destructive working-state deletion
record resequencing
nested Edit context
```

## State and recovery progression

```text
EXCLUDE
  -> display-state mutation

DELETE
  -> destructive working-data mutation
  -> CANCEL recovery

SORT
  -> working-data resequencing
  -> CANCEL recovery

Recursive Edit
  -> parent Edit suspended
  -> child Edit active
  -> child CANCEL
  -> parent Edit resumed
```

## Near-term roadmap

```text
Edit primary commands             VALIDATED
Advanced Edit primary commands    VALIDATED
CHANGE                            NEXT
Data storage / recovery           PLANNED
```
