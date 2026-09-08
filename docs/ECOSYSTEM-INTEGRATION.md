# MVS TSO/ISPF Ecosystem Integration

## Role

This repository provides the interactive entry point into the wider z/OS Engineering Laboratory.

Its responsibility is to establish the operator-facing foundations of TSO/E and ISPF before those capabilities are consumed by JCL, REXX, scheduler tooling, system operations and other repositories.

The repository focuses on how a user enters, navigates and works inside the z/OS interactive environment.

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

Provides the common ADCD/Hercules system context, engineering methodology and cross-repository architecture.

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

JCL work performed through ISPF depends on the editor, dataset navigation and interactive workflow introduced here.

Relationship:

```text
MVS_TSO_ISPF -> JCL_LABS
```

Status: **Foundational dependency**

### zos-batch-scheduler

Future scheduler operator interfaces and ISPF-oriented tools may consume the interactive environment established by this repository.

Relationship:

```text
MVS_TSO_ISPF -> REXX / ISPF services -> zos-batch-scheduler
```

Status: **Planned integration path**

### Other application and operations repositories

COBOL, Db2, CICS, VSAM, PL/I, Assembler and system-engineering labs frequently rely on TSO/E and ISPF as the operator interface used to edit members, navigate datasets, submit jobs and inspect results.

Status: **Shared interactive foundation**

## Consumes

This repository currently consumes:

- 3270/TN3270 interactive access;
- TSO/E;
- ISPF;
- partitioned and sequential datasets used during navigation and editing;
- the z/OS user session and command environment.

These are platform services. Their configuration and security are owned by other parts of the ecosystem.

## Produces

The repository currently produces:

- validated TSO/E logon workflow;
- native `READY` mode interaction;
- validated ISPF entry and navigation;
- direct-option and jump-navigation workflows;
- repeatable operator navigation patterns;
- security-reviewed evidence;
- documented interactive procedures.

Future labs are expected to extend this into dataset management, editor use, utilities, command interaction and automation prerequisites.

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
          |
          +--> jump function
          |
          +--> RETURN
```

Validated by Lab 02.

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

## Planned Cross-Repository Paths

The following are architectural targets and must not be interpreted as completed integrations.

### ISPF automation path

```text
MVS_TSO_ISPF
      |
      v
     REXX
      |
      v
ISPF services
      |
      v
operator automation
```

### Batch operator path

```text
MVS_TSO_ISPF
      |
      v
 dataset/member editing
      |
      v
     JCL
      |
      v
    JES2
```

### Scheduler operator path

```text
MVS_TSO_ISPF
      |
      v
REXX / ISPF services
      |
      v
zos-batch-scheduler
```

## Integration Status

| Integration | Status | Evidence |
| --- | --- | --- |
| 3270/TN3270 -> TSO/E | Validated | Lab 01 |
| TSO/E -> READY -> ISPF | Validated | Lab 01 |
| ISPF hierarchy/navigation | Validated | Lab 02 |
| MVS_TSO_ISPF -> REXX foundation | Validated foundation | REXX Labs 01-02 consume this environment |
| MVS_TSO_ISPF -> JCL workflow | Foundational | Used across batch-oriented labs |
| REXX -> ISPF services | Planned | Future REXX/ISPF work |
| MVS_TSO_ISPF -> scheduler operator tooling | Planned | Future integration |

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
Consume that environment from the specialized repositories.
Do not duplicate their domain-specific labs inside MVS_TSO_ISPF.
```

## Development Direction

The current progression is:

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
dataset/member work
     |
     v
editor and utilities
     |
     v
REXX / ISPF automation prerequisites
     |
     v
cross-repository operator workflows
```

Near-term work should continue building a solid operator foundation before adding automation or cross-repository tooling.

## Engineering and Publication Rules

Each lab should continue to record:

- objective;
- concepts;
- exact interactive flow;
- commands;
- observed results;
- evidence;
- security review;
- references.

Cross-repository work should follow the common engineering cycle:

```text
Build -> Execute -> Observe -> Diagnose -> Correct -> Validate -> Document
```

Before publication:

- validate technical results;
- preserve evidence where appropriate;
- distinguish validated functionality from roadmap targets;
- do not publish credentials, IP addresses, MAC addresses, terminal/network identifiers or host-side network details;
- use short-lived integration branches and merge completed work into `main`.

## Master Architecture

The broader ecosystem architecture is maintained in:

https://github.com/P-dot/zos-adcd-hercules-engineering-lab
