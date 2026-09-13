# MVS TSO/ISPF Ecosystem Integration

## Role

This repository provides the interactive entry point into the wider z/OS Engineering Laboratory.

Its responsibility is to establish the operator-facing foundations of TSO/E and ISPF before those capabilities are consumed by JCL, REXX, scheduler tooling, system operations and other repositories.

The repository focuses on how a user enters, navigates, inspects and works inside the z/OS interactive environment.

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

## Upstream Dependencies

### z/OS Engineering Laboratory

Provides the common ADCD/Hercules system context, engineering methodology, Architecture V1 repository relationships and Architecture V2 engineering classification.

Status: **Active architectural dependency**

### Communications Server environment

Interactive access depends on the availability of the 3270/TN3270 path provided by the wider z/OS communications environment.

This repository consumes that access path but does not own network configuration, TCP/IP policy or Communications Server administration.

Status: **Environment dependency**

## Downstream Consumers

### REXX

REXX consumes the TSO/E and ISPF environment established here.

Relationship:

```text
MVS_TSO_ISPF -> REXX
```

Status: **Validated foundation**

### JCL_LABS

JCL work performed through ISPF depends on the editor, dataset navigation, Browse and interactive workflow introduced here.

Relationship:

```text
MVS_TSO_ISPF -> JCL_LABS
```

Status: **Validated interactive foundation**

Labs 04 and 05 use `IBMUSER.JCL.LAB` as an ISPF data object. JCL semantics remain out of scope and continue to belong to `JCL_LABS`.

### zos-batch-scheduler

Future scheduler operator interfaces and ISPF-oriented tools may consume the interactive environment established by this repository.

Relationship:

```text
MVS_TSO_ISPF -> REXX / ISPF services -> zos-batch-scheduler
```

Status: **Planned integration path**

### Other application and operations repositories

COBOL, Db2, CICS, VSAM, PL/I, Assembler and system-engineering labs frequently rely on TSO/E and ISPF as the operator interface used to inspect members, edit source, navigate datasets, submit jobs and inspect results.

Status: **Shared interactive foundation**

## Produces

The repository currently produces:

- validated TSO/E logon workflow;
- native `READY` mode interaction;
- validated ISPF entry and navigation;
- direct-option and jump-navigation workflows;
- validated logical-screen operation with SPLIT, SWAP and SWAP LIST;
- validated DSLIST data-set discovery;
- validated partitioned-data-set member-list processing;
- validated read-only Browse navigation;
- validated scroll-amount control;
- validated Browse line-number and label-based positioning;
- repeatable operator navigation and inspection procedures;
- security-reviewed evidence.

## Validated Integration Paths

### Interactive access path

```text
3270 / TN3270
      |
      v
   TSO/E
      |
      v
    READY
      |
      v
    ISPF
```

Validated by Lab 01.

### ISPF navigation path

```text
ISPF Primary Option Menu
          |
          v
     panel hierarchy
          |
          +--> direct option entry
          +--> jump function
          +--> RETURN
```

Validated by Lab 02.

### Logical-screen operator path

```text
ISPF
 |
 +--> logical screen 1
 |
 +--> logical screen 2
        |
        +--> SWAP / SWAP LIST
```

Validated by Lab 03.

### Data set and member operator path

```text
TSO PROFILE
      |
      v
PREFIX(IBMUSER)
      |
      v
ISPF DSLIST
      |
      v
partitioned data set
      |
      v
member list
      |
      +--> SELECT
      +--> LOCATE
      +--> SORT
      +--> RESET
      +--> member pattern
```

Validated by Lab 04.

### Read-only Browse operator path

```text
PDS member list
      |
      v
BROWSE member
      |
      +--> PAGE / HALF
      +--> numeric scroll
      +--> MAX
      +--> LOCATE line
      +--> assign label
      +--> LOCATE label
      |
      v
END -> member list
```

Validated by Lab 05.

Lab 05 is a capability validation inside `MVS_TSO_ISPF`; it is not a cross-repository integration merely because the inspected member contains JCL.

### REXX foundation path

```text
MVS_TSO_ISPF
      |
      v
 TSO/E / ISPF
      |
      v
     REXX
```

The interactive foundation is validated here. REXX execution itself is validated in the REXX repository.

## Architecture V2 classification

New labs in this repository should record:

- engineering domain;
- capability;
- lifecycle stage;
- maturity level;
- integration level;
- dependencies;
- evidence;
- validation status;
- next capability.

The near-term capability progression is:

```text
dataset/member work
      |
      v
Browse fundamentals
      |
      v
advanced Browse commands
      |
      v
Browse FIND / RFIND
      |
      v
Edit
      |
      v
utilities
      |
      v
REXX / ISPF automation prerequisites
```

## Planned Cross-Repository Paths

### Operations Automation — Production Track 08

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

`MVS_TSO_ISPF` supplies the manual and operator-facing capability foundation. Automation belongs primarily to the repositories and tracks that own the automation logic.

### Batch operator path

```text
MVS_TSO_ISPF
      |
      v
dataset/member inspection and editing
      |
      v
JCL
      |
      v
JES2
```

Labs 04-05 validate navigation and read-only inspection prerequisites. Editing and submission remain later capabilities or belong to the specialized batch repository when the engineering objective is JCL/JES2 behavior.

## Integration Status

| Integration / capability path | Status | Evidence |
|---|---|---|
| 3270/TN3270 -> TSO/E | Validated | Lab 01 |
| TSO/E -> READY -> ISPF | Validated | Lab 01 |
| ISPF hierarchy/navigation | Validated | Lab 02 |
| ISPF logical-screen operation | Validated | Lab 03 |
| ISPF DSLIST -> PDS member list | Validated | Lab 04 |
| ISPF member list -> read-only Browse navigation | Validated | Lab 05 |
| MVS_TSO_ISPF -> REXX foundation | Validated foundation | REXX labs consume this environment |
| MVS_TSO_ISPF -> JCL workflow | Validated interactive foundation | JCL semantics remain in JCL_LABS |
| REXX -> ISPF services | Planned | Future REXX/ISPF work |
| MVS_TSO_ISPF -> scheduler operator tooling | Planned | Production Track 08 |

## Scope Boundaries

This repository owns interactive TSO/E and ISPF foundations.

It does **not** replace:

- `Rexx` for REXX language and automation logic;
- `JCL_LABS` for JCL semantics and batch execution;
- `zos-batch-scheduler` for scheduling and orchestration;
- `zos-communications-server-network-lab` for TCP/IP, TN3270 service configuration and network security;
- `mainframe-racf-security-evidence` for RACF administration and access-control policy;
- the core z/OS Engineering Laboratory for system-level engineering.

The integration rule is:

```text
Learn and validate the interactive environment here.
Consume that environment from specialized repositories.
Do not duplicate their domain-specific labs inside MVS_TSO_ISPF.
```

## Development Direction

```text
TSO/E logon
     |
     v
READY mode
     |
     v
ISPF entry
     |
     v
ISPF navigation
     |
     v
logical-screen operation
     |
     v
dataset/member work
     |
     v
Browse fundamentals
     |
     v
advanced Browse / Find
     |
     v
Edit and utilities
     |
     v
REXX / ISPF automation prerequisites
     |
     v
cross-repository operator workflows
```

Labs 01-05 validate the path through read-only Browse fundamentals.

## Engineering and Publication Rules

Each new lab should record:

- Architecture V2 metadata;
- objective;
- engineering context;
- scope and preconditions;
- exact interactive flow;
- commands;
- expected result;
- observed result;
- evidence;
- failure or exception analysis where appropriate;
- recovery/rollback;
- publication-security review;
- cross-repository relationships;
- next capability;
- references.

The common engineering cycle remains:

```text
Build -> Execute -> Observe -> Diagnose -> Correct -> Validate -> Document
```

Before publication:

- validate technical results;
- preserve evidence where appropriate;
- distinguish validated functionality from roadmap targets;
- do not publish credentials, IP addresses, MAC addresses, terminal/network identifiers or host-side network details;
- use short-lived lab/integration branches and merge completed work into `main`.

## Master Architecture

The broader ecosystem architecture and Architecture V2 are maintained in:

https://github.com/P-dot/zos-adcd-hercules-engineering-lab
