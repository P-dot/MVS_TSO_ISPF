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
```

## Controlled Edit capability path

```text
Lab 08
persistent state control
SAVE / CANCEL / restore
        |
        v
Lab 09
record mutation semantics
I / I3 / D / D3 / DD
        |
        v
Lab 10
Repeat / Copy / Move / A / B
```

Lab 09 uses `IBMUSER.ISPF.LAB(EDIT09)` with a canonical baseline under `fixtures/edit/EDIT09-baseline.txt`.

The lab validates record-count transitions and then uses `CANCEL` plus independent Browse to prove that the persistent fixture returns to its 13-record baseline.

It also validates safe handling of a pending block delete:

```text
DD
 |
 v
Block command incomplete
 |
RESET
 |
 v
pending command cleared
records preserved
```

## Cross-repository boundary

State-changing Edit labs operate only on `IBMUSER.ISPF.LAB`.

A future `ISPF Edit -> JCL -> SUBMIT -> JES2 -> SDSF` flow will be treated as explicit cross-repository integration.

## Near-term roadmap

```text
Controlled Edit lifecycle        VALIDATED
INSERT / DELETE line commands    VALIDATED
Repeat / Copy / Move / A / B     NEXT
advanced Edit / utilities        PLANNED
REXX / ISPF automation           PLANNED
```

## Master Architecture

https://github.com/P-dot/zos-adcd-hercules-engineering-lab
