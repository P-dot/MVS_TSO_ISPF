# MVS TSO/ISPF Ecosystem Integration

## Role

This repository provides the interactive entry point into the wider z/OS Engineering Laboratory.

Its responsibility is to establish the operator-facing foundations of TSO/E and ISPF before those capabilities are consumed by JCL, REXX, scheduler tooling, system operations and other repositories.

```text
3270 / TN3270
      |
      v
   TSO/E
      |
      v
    ISPF
      |
      +------> JCL_LABS
      |
      +------> REXX
                  |
                  v
          ISPF automation
```

## Architecture V2 responsibility

`MVS_TSO_ISPF` owns the interactive operator foundation:

- TSO/E interaction;
- ISPF navigation;
- logical screens;
- data-set/member navigation;
- Browse;
- future Edit and utility productivity;
- prerequisites for ISPF/REXX automation.

It does not own JCL semantics, REXX language logic, RACF policy, Communications Server configuration or scheduler orchestration.

## Validated capability progression

```text
Lab 01
TSO/E -> READY -> ISPF
        |
        v
Lab 02
ISPF hierarchy / direct navigation
        |
        v
Lab 03
logical screens / SWAP
        |
        v
Lab 04
DSLIST / PDS member lists
        |
        v
Lab 05
Browse navigation / positioning
        |
        v
Lab 06
Browse representation / HEX / recursive Browse
```

## Validated Browse path

### Browse navigation — Lab 05

```text
PDS member list
      |
      v
BROWSE
      |
      +--> PAGE / HALF / numeric / MAX
      +--> LOCATE line
      +--> temporary label
      +--> LOCATE label
```

### Browse representation and nesting — Lab 06

```text
BROWSE
   |
   +--> COLUMNS
   |      |
   |      +--> RESET
   |
   +--> DISPLAY CC / NOCC
   |
   +--> HEX ON VERT
   |      |
   |      +--> HEX ON DATA
   |      |
   |      +--> HEX OFF
   |
   +--> BROWSE another member
          |
          v
      recursive Browse
          |
          v
        END
          |
          v
      parent Browse
```

Lab 06 validates read-only display transformation and nested inspection. It does not modify the underlying PDS member.

## Cross-repository relationships

### JCL_LABS

`IBMUSER.JCL.LAB` supplies real data for Labs 04–06.

Relationship:

```text
MVS_TSO_ISPF -> interactive inspection of JCL artifacts
JCL_LABS     -> JCL semantics / JES2 behavior
```

The use of a JCL member as test data does not make Lab 06 a cross-repository integration proof.

### REXX

The manual Browse capabilities form part of the prerequisite chain for later ISPF service automation:

```text
MVS_TSO_ISPF
      |
      v
manual ISPF capability
      |
      v
REXX / ISPF services
      |
      v
Operations Automation
```

Status: **foundation only; automation not yet implemented here**

## Architecture V2 classification rule

New labs should record:

- engineering domain;
- capability;
- lifecycle stage;
- maturity level;
- integration level;
- dependencies;
- validation status;
- evidence;
- next capability.

## Near-term roadmap

```text
Browse navigation              VALIDATED
        |
        v
Browse representation / HEX    VALIDATED
        |
        v
Browse FIND / RFIND            NEXT
        |
        v
Edit
        |
        v
ISPF utilities
        |
        v
REXX / ISPF automation prerequisites
        |
        v
cross-repository operator workflows
```

## Production Track relationship

Architecture V2 Production Track 08 — Operations Automation remains a planned higher-level consumer:

```text
TSO / ISPF
    |
    v
REXX
    |
    v
Operational procedure
    |
    v
Scheduler / USS / z/OSMF
    |
    v
REST / External Automation
```

Labs in this repository first establish manual capability depth before automation is introduced.

## Engineering and publication rules

Each new lab should record:

- Architecture V2 metadata;
- objective and scope;
- preconditions;
- exact interactive flow;
- expected and observed result;
- evidence;
- failure/exception analysis where appropriate;
- rollback/recovery;
- security/publication review;
- cross-repository relationships;
- next capability;
- references.

Use short-lived branches:

```text
lab/<number>-<slug>
docs/<topic>
integration/<track>
fix/<topic>
```

`main` remains the validated published state.

## Master Architecture

The broader ecosystem architecture and Architecture V2 are maintained in:

https://github.com/P-dot/zos-adcd-hercules-engineering-lab
