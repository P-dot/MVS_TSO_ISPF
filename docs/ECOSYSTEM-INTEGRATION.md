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
- controlled Edit behavior;
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
        |
        v
Lab 07
Browse FIND / RFIND / targeted search
        |
        v
Lab 08
controlled Edit / SAVE / CANCEL / restore
```

## Browse capability block

Labs 05–07 validate read-only navigation, representation and targeted search.

```text
Browse navigation
      |
      v
Browse representation
      |
      v
Browse search
```

Lab 07 closes the current read-only Browse block.

## Controlled Edit path — Lab 08

Lab 08 introduces state-changing ISPF work using a repository-owned fixture.

```text
known baseline
      |
      v
Edit working state
      |
      +---- CANCEL ----> baseline preserved
      |
      +---- SAVE ------> change persisted
                              |
                              v
                       controlled restore
                              |
                              v
                       baseline revalidated
```

The fixture is isolated in:

```text
IBMUSER.ISPF.LAB(EDIT08)
```

with a canonical repository copy:

```text
fixtures/edit/EDIT08-baseline.txt
```

This avoids making state-changing ISPF experiments against JCL, COBOL, REXX or other repository-owned artifacts.

## Cross-repository relationships

### JCL_LABS

`IBMUSER.JCL.LAB` supplied real read-only data for Labs 04–07.

Relationship:

```text
MVS_TSO_ISPF -> interactive inspection/search of JCL artifacts
JCL_LABS     -> JCL semantics / JES2 behavior
```

Beginning with state-changing Edit labs, `MVS_TSO_ISPF` uses its own fixture library. Future cross-repository modification or SUBMIT flows must be designed explicitly as integration labs rather than silently reusing another repository's artifacts.

### REXX

The manual ISPF capabilities form part of the prerequisite chain for later ISPF service automation:

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

## Near-term roadmap

```text
Browse navigation                VALIDATED
        |
        v
Browse representation / HEX      VALIDATED
        |
        v
Browse FIND / RFIND              VALIDATED
        |
        v
Controlled Edit lifecycle        VALIDATED
        |
        v
Edit line-command fundamentals   NEXT
        |
        v
advanced Edit / utilities
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
