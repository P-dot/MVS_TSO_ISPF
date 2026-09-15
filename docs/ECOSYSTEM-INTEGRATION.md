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
Lab 10  Repeat / Copy / Move / Before / After
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
record replication and relocation
R / C / M / A / B
        |
        v
Lab 11
MASK / OVERLAY
```

Lab 10 uses `IBMUSER.ISPF.LAB(EDIT10)` with a canonical baseline under:

```text
fixtures/edit/EDIT10-baseline.txt
```

The lab validates working-state transformations, cardinality rules, destination placement, pending source/destination state, a real command-conflict negative test, and rollback to the 28-record persistent baseline.

## Cross-repository boundary

State-changing Edit labs operate only on `IBMUSER.ISPF.LAB`.

A future:

```text
ISPF Edit -> JCL -> SUBMIT -> JES2 -> SDSF
```

will be treated as explicit cross-repository integration.

## Near-term roadmap

```text
Controlled Edit lifecycle        VALIDATED
INSERT / DELETE line commands    VALIDATED
Repeat / Copy / Move / A / B     VALIDATED
MASK / OVERLAY                    NEXT
advanced Edit / utilities         PLANNED
REXX / ISPF automation            PLANNED
```

## Master Architecture

https://github.com/P-dot/zos-adcd-hercules-engineering-lab
