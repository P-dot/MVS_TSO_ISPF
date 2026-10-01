# MVS TSO/ISPF Ecosystem Integration

## Purpose

This document defines the role of `MVS_TSO_ISPF` inside the wider IBM z/OS engineering portfolio.

The repository owns the **interactive TSO/E and ISPF capability track**. Its validated evidence currently spans the complete progression from entering a TSO/E session through advanced ISPF Edit operations and controlled recovery of working state.

The repository is not a generic container for every technology that can be reached from ISPF.

## Repository Ownership

Owned here:

```text
TSO/E interactive session
native READY environment
ISPF entry / exit
ISPF navigation
direct options and jump navigation
RETURN / END behavior
logical screens
SPLIT / SWAP
data-set discovery
PDS member-list interaction
Browse navigation
Browse display controls
Browse search
Edit lifecycle
Edit line commands
Edit primary commands
display-state mutation
working-data mutation
CANCEL-based recovery
nested Browse / Edit context
```

Not owned here:

```text
JCL language semantics
JES2 execution lifecycle
batch scheduling
REXX language / automation architecture
USS administration
RACF administration
Communications Server configuration
COBOL / PL/I / HLASM language engineering
VSAM architecture
Db2 architecture
CICS administration
system-wide recovery
```

The distinction is based on **capability ownership**, not on which technology happens to appear on an ISPF screen.

## Validated Capability Progression

### Stage A — TSO/E session foundation

```text
Lab 01
3270 / TN3270
      |
      v
TSO/E logon
      |
      +--> ISPF
      |     |
      |     +--> ISPF Command Shell
      |            |
      |            +--> TSO PROFILE
      |
      +--> native READY
              |
              +--> TSO PROFILE
              |
              +--> LOGOFF
```

Validated capability:

- TSO/E logon flow;
- ISPF running within the TSO/E session;
- ISPF Command Shell;
- transition from ISPF to native `READY`;
- native TSO command execution;
- explicit `LOGOFF`.

This establishes the session model used by every later interactive lab.

### Stage B — ISPF navigation and work contexts

```text
Lab 02
hierarchical navigation
   -> direct option
   -> jump function
   -> END / F3
   -> RETURN

Lab 03
single ISPF session
   -> SPLIT
   -> multiple logical screens
   -> SWAP
   -> SWAP LIST
   -> independent panel state
```

Validated capability:

- panel hierarchy;
- direct navigation;
- jump navigation;
- navigation-stack behavior;
- logical-screen creation and switching;
- independent work context inside one ISPF session.

### Stage C — Data-set and member interaction

```text
Lab 04
TSO prefix
   -> DSLIST
   -> data-set qualifiers
   -> PDS
   -> member list
   -> LOCATE / SORT / RESET / filtering
```

The repository owns the **interactive discovery and member-list behavior**.

A member may contain JCL or source code, but that does not transfer ownership of the underlying language or execution domain to ISPF.

### Stage D — Read-only inspection

```text
Lab 05
Browse navigation
   -> scrolling
   -> positioning
   -> LOCATE
   -> labels

Lab 06
display controls
   -> COLUMNS
   -> DISPLAY CC / NOCC
   -> HEX representation
   -> Recursive Browse
   -> parent context restoration

Lab 07
FIND
   -> RFIND
   -> ALL
   -> FIRST / LAST
   -> string context
   -> column-scoped search
```

This stage is intentionally read-only.

Architecture characteristics represented in the current lab metadata include:

```text
Lifecycle: Operate / Observe
Maturity: M1 — Foundational
Integration: I0 — Standalone
Persistent change: NONE
```

## Controlled Edit Progression

### Lab 08 — Edit transaction lifecycle

Lab 08 is the transition from observation to controlled mutation.

```text
Baseline
   |
   v
Edit
   |
   +--> modify
   |
   +--> CANCEL ----> baseline preserved/restored
   |
   +--> SAVE ------> persistent state
```

The lab validates controlled modification, persistence behavior, rollback and post-recovery verification.

Architecture classification in the lab:

```text
Lifecycle:
Baseline / Configure / Operate / Observe / Recover

Maturity:
M3 — Resilient

Integration:
I0 — Standalone
```

The M3 classification applies to the demonstrated controlled Edit capability, not to the repository as a whole.

### Lab 09 — INSERT and DELETE

Validated:

```text
single INSERT
numeric INSERT
single DELETE
numeric DELETE
block DELETE
incomplete block-command handling
RESET
CANCEL recovery
independent baseline verification
```

The lab uses deterministic record-count transitions rather than visual success alone.

### Lab 10 — Repeat, Copy and Move

Validated:

```text
Repeat
Copy
Move
A / B destination semantics
numeric destination repetition
pending COPY / MOVE state
multiple line commands
controlled conflict handling
rollback after mutation transactions
```

### Lab 11 — MASK, OVERLAY and COLS

Validated capability:

```text
templated insertion
controlled overlay merge
column-position inspection
negative/protective behavior
state restoration
```

### Lab 12 — BNDS and shifting

Validated capability:

```text
BNDS inspection
controlled boundary configuration
column shifting
destructive shifting
data-shifting protection
incomplete-shift diagnostics
RESET
block shifting
profile restoration
final persistent-state validation
```

### Lab 13 — EXCLUDE, labels and TABS

Validated capability:

```text
selective visibility
partial redisplay
SHOW behavior
session labels
built-in positional labels
TABS special-line state
persistent member unchanged
```

Architecture classification:

```text
M2 — Operational
I0 — Standalone
```

### Lab 14 — Edit primary commands

Validated repository-owned behavior:

```text
HEX
FIND
LOCATE
selective RESET
```

`SUBMIT` is an important architectural boundary.

ISPF can expose the command, but the execution path:

```text
ISPF
  -> JCL
  -> JES2
```

crosses into the JCL/JES2 domain. Standalone ISPF evidence must not be presented as end-to-end batch validation unless that path has actually been exercised and documented as an integration scenario.

### Lab 15 — Advanced primary commands

Validated:

```text
content-driven EXCLUDE
label-range EXCLUDE
DELETE of excluded working data
CANCEL recovery
SORT over controlled range
CANCEL recovery of original sequence
Recursive Edit
child CANCEL
return to parent Edit context
```

State progression:

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

Architecture classification:

```text
M3 — Resilient
I0 — Standalone
```

M3 is supported for this scoped capability by observed destructive/resequencing working-state mutation followed by explicit rollback and verified context recovery.

## Capability Map

```text
TSO/E SESSION
    |
    +-- Lab 01
    |
    v
ISPF NAVIGATION
    |
    +-- Lab 02
    +-- Lab 03
    |
    v
DATA-SET / MEMBER INTERACTION
    |
    +-- Lab 04
    |
    v
READ-ONLY INSPECTION
    |
    +-- Lab 05
    +-- Lab 06
    +-- Lab 07
    |
    v
CONTROLLED EDIT
    |
    +-- Lab 08
    +-- Lab 09
    +-- Lab 10
    +-- Lab 11
    +-- Lab 12
    |
    v
ADVANCED EDIT
    |
    +-- Lab 13
    +-- Lab 14
    +-- Lab 15
    |
    v
NEXT CAPABILITY
    |
    +-- CHANGE
```

## State Model

The repository increasingly distinguishes three forms of state:

```text
DISPLAY STATE
    |
    |  examples:
    |  EXCLUDE
    |  HEX display
    |  labels
    |  TABS special line
    |
    v

WORKING DATA
    |
    |  examples:
    |  INSERT
    |  DELETE
    |  MOVE
    |  OVERLAY
    |  SORT
    |
    +--> CANCEL
    |      |
    |      +--> discard / recover working mutation
    |
    +--> SAVE
           |
           +--> persistent data

PERSISTENT DATA
```

This distinction prevents a common documentation error: treating a visible panel change, an unsaved Edit mutation and a persisted data change as equivalent events.

## Architecture V2 Relationship

The portfolio lifecycle is:

```text
Discover
   -> Baseline
   -> Configure
   -> Operate
   -> Observe
   -> Diagnose
   -> Recover
   -> Improve
   -> Automate
   -> Integrate
```

The early labs primarily establish Discover / Operate / Observe behavior.

The Edit track introduces controlled Baseline / Configure / Recover behavior.

Individual lab metadata may therefore progress from:

```text
M1 — Foundational
      |
      v
M2 — Operational
      |
      v
M3 — Resilient
```

This is **capability-scoped maturity**.

It does not mean that the complete TSO/E and ISPF domain has reached M3, nor does it imply system-wide resilience.

The current standalone labs are generally:

```text
I0 — Standalone
```

because the validated execution remains within repository-owned TSO/E and ISPF behavior.

## Evidence Model

Evidence should answer more than:

> Did the command run?

For state-changing capabilities, the stronger model is:

```text
KNOWN BASELINE
      |
      v
CONTROLLED ACTION
      |
      v
OBSERVED TRANSITION
      |
      +--> expected behavior
      |
      +--> negative / protective behavior
      |
      v
RECOVERY
      |
      v
INDEPENDENT VALIDATION
```

Examples already demonstrated across the repository include:

- deterministic fixtures;
- explicit record counts;
- incomplete block-command behavior;
- environment-specific syntax behavior;
- working-state deletion;
- working-state resequencing;
- `CANCEL` rollback;
- parent/child recursive-context recovery;
- final baseline verification.

For interactive-only capabilities:

```text
batch RC = NOT APPLICABLE
```

A return code must not be invented simply to make the evidence resemble a batch lab.

## Cross-Repository Boundaries

### JCL / JES2

Relationship:

```text
MVS_TSO_ISPF
    |
    | interactive discovery / Browse / Edit
    v
JCL_LABS
    |
    | JCL semantics / submission / execution
    v
JES2
```

Validated locally:

```text
ISPF data-set/member interaction
ISPF Browse/Edit behavior
```

Cross-domain execution:

```text
ISPF -> JCL -> JES2
```

must be classified separately and validated by the appropriate integration evidence.

### REXX

Relationship:

```text
manual TSO/E / ISPF operation
          |
          v
        REXX
          |
          v
interactive automation / ISPF services
```

This repository provides the human-operated baseline that automation can later consume.

REXX language semantics and automation implementation remain owned by the REXX repository.

### USS

TSO/E and ISPF are one interactive operating surface of z/OS. USS is another.

```text
interactive z/OS operation
       |
       +--> TSO/E / ISPF
       |
       +--> USS
```

USS shell behavior, files, processes and administration remain owned by the USS repository.

### Application and data repositories

COBOL, PL/I, HLASM, VSAM, Db2 and CICS artifacts may be inspected or edited through ISPF.

That is a supporting operator capability, not proof that `MVS_TSO_ISPF` owns those technologies.

## Local Validation vs Ecosystem Validation

Architecture V2 should preserve the distinction:

```text
VALIDATED LOCALLY
        !=
VALIDATED IN PORTFOLIO / ECOSYSTEM
        !=
PLANNED
```

For this repository:

```text
TSO/E session model ....................... VALIDATED LOCALLY
ISPF navigation ........................... VALIDATED LOCALLY
data-set/member interaction ............... VALIDATED LOCALLY
Browse inspection ......................... VALIDATED LOCALLY
controlled Edit / recovery ................ VALIDATED LOCALLY
advanced Edit operations .................. VALIDATED LOCALLY

CHANGE .................................... NEXT

ISPF -> JCL -> JES2 end-to-end path ....... CROSS-DOMAIN / requires its own evidence
REXX automation of ISPF workflow .......... PLANNED / separate track unless evidenced
broader production integration ............ PLANNED / separate track unless evidenced
```

No integration state should be upgraded merely because a related repository exists.

## Portfolio Role

This repository is the operational foundation for the first stage of the portfolio learning journey.

```text
CONTROL THE ENVIRONMENT
        |
        v
TSO/E
        |
        v
ISPF
        |
        +--> navigation
        +--> data sets
        +--> Browse
        +--> Edit
        |
        v
JCL / JES2
        |
        v
workload operation
        |
        v
automation / application / data / security / diagnostics
```

This makes `MVS_TSO_ISPF` a **foundation repository**, not an integration repository.

Its purpose is to prove that the operator can control the interactive environment safely and reproducibly before higher-level workflows depend on it.

## Repository Structure

```text
MVS_TSO_ISPF/
|
+-- README.md
+-- docs/
|   +-- ECOSYSTEM-INTEGRATION.md
|
+-- fixtures/
|   +-- edit/
|
+-- labs/
|   +-- 01 ... TSO/E session
|   +-- 02 ... ISPF navigation
|   +-- 03 ... logical screens
|   +-- 04 ... data sets / members
|   +-- 05 ... Browse navigation
|   +-- 06 ... Browse display / HEX / recursion
|   +-- 07 ... Browse search
|   +-- 08 ... controlled Edit lifecycle
|   +-- 09 ... INSERT / DELETE
|   +-- 10 ... Repeat / Copy / Move
|   +-- 11 ... MASK / OVERLAY / COLS
|   +-- 12 ... BNDS / shifting
|   +-- 13 ... EXCLUDE / labels / TABS
|   +-- 14 ... primary commands
|   +-- 15 ... advanced primary commands
|
+-- references/
```

## Current Validated Boundary

Current endpoint:

```text
Lab 15
Advanced ISPF Edit primary commands

EXCLUDE
DELETE
SORT
Recursive Edit
working-state recovery
nested-context recovery
```

Near-term roadmap:

```text
TSO/E / ISPF session foundation     VALIDATED
ISPF navigation                     VALIDATED
data-set/member interaction         VALIDATED
Browse                              VALIDATED
controlled Edit                     VALIDATED
advanced Edit primary commands      VALIDATED
CHANGE                              NEXT
broader data storage/recovery       PLANNED
cross-repository production paths   PLANNED unless separately evidenced
```

## Publication Security

Before evidence is published, review for:

```text
passwords / credentials
tokens / keys
private IP addresses
MAC addresses
host adapter identifiers
unnecessary terminal/session identifiers
sensitive host/network configuration
```

The objective is not to remove useful engineering evidence. It is to publish only the operational information required to demonstrate the capability.

## Engineering Principle

The repository should document:

> **what TSO/E and ISPF actually did in the tested environment**

rather than what a command or panel was expected to do.

Observed environment-specific behavior, protective responses, failed attempts and recovery paths are engineering evidence and should be preserved when they materially explain the validated capability.
