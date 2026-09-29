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
```

## Lab 14 ownership

Repository-owned capability:

```text
interactive display
search scope
positioning
session-state reset
```

Cross-repository boundary:

```text
SUBMIT
  |
  v
JCL / JES2
```

Lab 14 does not duplicate JCL or JES2 validation.

## Near-term roadmap

```text
Edit primary commands             VALIDATED
Advanced Edit primary commands    NEXT
CHANGE                            PLANNED
Data storage / recovery           PLANNED
```
