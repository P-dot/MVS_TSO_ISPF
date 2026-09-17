# MVS TSO/ISPF Ecosystem Integration

## Validated capability progression

```text
Lab 01  TSO/E -> READY -> ISPF
Lab 02  navigation hierarchy
Lab 03  logical screens / SWAP
Lab 04  DSLIST / PDS members
Lab 05  Browse navigation
Lab 06  Browse representation / HEX / recursive Browse
Lab 07  Browse FIND / RFIND
Lab 08  controlled Edit / SAVE / CANCEL / restore
Lab 09  INSERT / DELETE
Lab 10  Repeat / Copy / Move / A / B
Lab 11  MASK / OVERLAY / COLS
Lab 12  BNDS / column shifting / data shifting
```

## Controlled Edit capability path

```text
Lab 08  persistent-state control
Lab 09  record mutation
Lab 10  replication and relocation
Lab 11  templated input, overlay and column indicators
Lab 12  bounded positional transformation and shifting
Lab 13  EXCLUDE / labels / TABS
```

Lab 12 uses:

```text
IBMUSER.ISPF.LAB(EDIT12)
```

with canonical baseline:

```text
fixtures/edit/EDIT12-baseline.txt
```

The lab validates both dataset working-state behavior and BNDS/Edit Profile state, including destructive and protective shift behavior.

## Near-term roadmap

```text
MASK / OVERLAY / COLS             VALIDATED
BNDS / shifting                   VALIDATED
EXCLUDE / Edit labels / TABS      NEXT
Edit primary commands             PLANNED
REXX / ISPF automation            PLANNED
```

## Cross-repository boundary

State-changing Edit labs operate only on `IBMUSER.ISPF.LAB`.

Future `ISPF Edit -> JCL -> SUBMIT -> JES2 -> SDSF` work remains an explicit cross-repository integration scenario.

## Master Architecture

https://github.com/P-dot/zos-adcd-hercules-engineering-lab
