# MVS TSO/ISPF Ecosystem Integration

## Role

This repository provides the interactive entry point into the wider z/OS Engineering Laboratory.

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
Lab 09  INSERT / DELETE line commands
Lab 10  Repeat / Copy / Move / A / B
Lab 11  MASK / OVERLAY / COLS
```

## Controlled Edit capability path

```text
Lab 08  persistent-state control
Lab 09  record insertion/deletion
Lab 10  replication and relocation
Lab 11  templated input, merge and column positioning
Lab 12  BNDS and shifting
```

Lab 11 uses:

```text
IBMUSER.ISPF.LAB(EDIT11)
```

with canonical baseline:

```text
fixtures/edit/EDIT11-baseline.txt
```

The lab validates both dataset working-state behavior and Edit Profile mask state, then restores both.

## Cross-repository boundary

State-changing Edit labs operate only on `IBMUSER.ISPF.LAB`.

Future `ISPF Edit -> JCL -> SUBMIT -> JES2 -> SDSF` work remains an explicit integration scenario.

## Near-term roadmap

```text
Controlled Edit lifecycle        VALIDATED
INSERT / DELETE                   VALIDATED
Repeat / Copy / Move / A / B     VALIDATED
MASK / OVERLAY / COLS             VALIDATED
BNDS / shifting                   NEXT
advanced Edit / utilities         PLANNED
REXX / ISPF automation            PLANNED
```

## Master Architecture

https://github.com/P-dot/zos-adcd-hercules-engineering-lab
