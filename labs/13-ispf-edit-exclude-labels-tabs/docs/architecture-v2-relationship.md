# Architecture V2 Relationship

## Why this lab exists

Architecture V2 selects labs using:

```text
Domain roadmap
      +
Capability gap
      +
Lifecycle gap
      +
Integration roadmap
      |
      v
Next laboratory
```

Lab 13 fills the next MVS/TSO/ISPF capability gap after bounded Edit transformation.

## Domain ownership

```text
Domain:
Operations and Service Management

Repository:
MVS_TSO_ISPF

Capability:
Selective Edit visibility,
session-scoped positioning,
special-line state inspection
```

The fact that future automation may consume these behaviors does not move ownership to REXX.

## Downstream integration

The validated capability becomes a prerequisite for the broader Operations Automation production path:

```text
MVS / TSO / ISPF
      |
      v
REXX
      |
      v
operational procedures
      |
      v
scheduler / USS / z/OSMF
      |
      v
external automation
```

Lab 13 remains I0 because it validates one repository-owned capability.

Cross-repository proof belongs to a later Production Track.
