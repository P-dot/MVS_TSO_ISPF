# MVS TSO/ISPF Ecosystem Integration

## Repository ownership

`MVS_TSO_ISPF` owns interactive TSO/E and ISPF capability validation:

```text
TSO/E interaction
ISPF navigation
Browse
Edit
member-list productivity
interactive session state
future ISPF service prerequisites
```

It does not duplicate the curricula owned by JCL, JES2, REXX, diagnostics, security, scheduler or application repositories.

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
Lab 13  EXCLUDE / labels / TABS display state
```

## Controlled Edit capability path

```text
Lab 08  persistent-state control
Lab 09  record mutation
Lab 10  replication and relocation
Lab 11  templated input / overlay / column inspection
Lab 12  bounded positional transformation
Lab 13  selective visibility / session labels / special-line state
```

Lab 13 uses:

```text
IBMUSER.ISPF.LAB(EDIT13)
```

with canonical baseline:

```text
fixtures/edit/EDIT13-baseline.txt
```

The lab keeps three state domains separate:

```text
persistent dataset data
display state (excluded/visible)
session labels / position
special-line display state
```

## Architecture V2 relationship

Primary engineering domain:

```text
Operations and Service Management
```

Current integration level:

```text
I0 — Standalone
```

Downstream Architecture V2 relationship:

```text
MVS / TSO / ISPF
      |
      v
REXX
      |
      v
Production Track 08 — Operations Automation
```

This repository validates the interactive capability. The production track later proves cross-repository automation and operational integration.

## Near-term roadmap

```text
MASK / OVERLAY / COLS             VALIDATED
BNDS / shifting                   VALIDATED
EXCLUDE / labels / TABS           VALIDATED
Edit primary commands             NEXT
REXX / ISPF automation            PLANNED
```

## Cross-repository boundary

Future workflows such as:

```text
ISPF -> JCL -> SUBMIT -> JES2 -> SDSF
```

are cross-repository integration scenarios. They should reference validated domain capabilities rather than duplicate complete JCL/JES2 labs here.

## Master Architecture

https://github.com/P-dot/zos-adcd-hercules-engineering-lab
