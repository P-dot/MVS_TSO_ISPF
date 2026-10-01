# MVS TSO/ISPF — Interactive z/OS Operations Labs

Hands-on engineering repository for **TSO/E and ISPF interactive operations on z/OS**, built from validated laboratory evidence rather than command-reference summaries.

This repository is the interactive entry point into the wider IBM z/OS engineering portfolio. It establishes the operator workflow used to navigate the system, inspect data sets, work with members, perform controlled editing, recover working state, and hand work off to specialized domains such as JCL/JES2 and REXX.

> **Current validated scope:** Labs 01–15
> **Next capability:** ISPF Edit `CHANGE`
> **Architecture:** Portfolio Navigation V2 / Engineering Control

## Navigate

- [Lab 01 — TSO/E Logon, READY and ISPF Environment](labs/01-tso-e-logon-ready-ispf-environment/)
- [Lab 02 — ISPF Navigation, Hierarchy, Direct Options and RETURN](labs/02-ispf-navigation-hierarchy-direct-options-return/)
- [Lab 03 — ISPF Split Screen, SWAP and Logical Screens](labs/03-ispf-split-screen-swap-logical-screens/)
- [Lab 04 — ISPF Data Set Names and Member Lists](labs/04-ispf-dataset-names-member-lists/)
- [Lab 05 — Browse Navigation, Scrolling, LOCATE and Labels](labs/05-ispf-browse-navigation-scrolling-locate-labels/)
- [Lab 06 — Browse Display Controls, HEX and Recursive Browse](labs/06-ispf-browse-display-hex-recursive/)
- [Lab 07 — Browse FIND, RFIND and Search Controls](labs/07-ispf-browse-find-rfind-search-controls/)
- [Lab 08 — Controlled Edit, SAVE, CANCEL and Restore](labs/08-ispf-edit-controlled-save-cancel-restore/)
- [Lab 09 — Edit INSERT and DELETE](labs/09-ispf-edit-insert-delete-line-commands/)
- [Lab 10 — Edit Repeat, Copy, Move, Before and After](labs/10-ispf-edit-repeat-copy-move-before-after/)
- [Lab 11 — Edit MASK, OVERLAY and COLS](labs/11-ispf-edit-mask-overlay-cols/)
- [Lab 12 — Edit BNDS and Data Shifting](labs/12-ispf-edit-bnds-column-data-shifting/)
- [Lab 13 — Edit EXCLUDE, Labels and TABS](labs/13-ispf-edit-exclude-labels-tabs/)
- [Lab 14 — Edit HEX, FIND, LOCATE and RESET](labs/14-ispf-edit-primary-commands/)
- [Lab 15 — Edit EXCLUDE, DELETE, SORT and Recursive Edit](labs/15-ispf-edit-advanced-primary-commands/)
- [Ecosystem Integration](docs/ECOSYSTEM-INTEGRATION.md)
- [Portfolio](https://github.com/P-dot)

## Repository Role

`MVS_TSO_ISPF` owns the **interactive TSO/E and ISPF operating layer** of the portfolio.

It demonstrates how an operator moves from a 3270 session into TSO/E, enters and leaves ISPF, navigates panels and logical screens, discovers data sets and members, performs read-only inspection, modifies controlled fixtures, and restores state after destructive working-session operations.

```text
3270 / TN3270
      |
      v
    TSO/E
      |
      +--> native READY environment
      |
      v
     ISPF
      |
      +--> navigation / logical screens
      +--> data-set and member interaction
      +--> Browse
      +--> Edit
      |
      +----------------------> specialized repositories
                                JCL / JES2
                                REXX
                                USS
                                application and data domains
```

The repository does **not** claim ownership of JCL semantics, JES2 processing, scheduler logic, RACF administration, Communications Server configuration, application-language development, or data-engine architecture.

## Capability Progression

```text
SESSION
  Lab 01
  TSO/E -> ISPF -> READY -> LOGOFF
       |
       v
NAVIGATION
  Labs 02-03
  hierarchy -> direct options -> RETURN -> SPLIT -> SWAP
       |
       v
DATA-SET INTERACTION
  Lab 04
  DSLIST -> qualifiers -> PDS -> members
       |
       v
READ-ONLY INSPECTION
  Labs 05-07
  Browse -> positioning -> HEX -> recursive Browse -> FIND/RFIND
       |
       v
CONTROLLED EDIT
  Labs 08-12
  SAVE/CANCEL -> INSERT/DELETE -> COPY/MOVE -> MASK/OVERLAY -> BNDS
       |
       v
ADVANCED EDIT
  Labs 13-15
  EXCLUDE -> labels -> search -> RESET -> DELETE -> SORT -> recursive Edit
       |
       v
NEXT
  CHANGE
```

This progression moves from **safe observation** to **controlled mutation and recovery**.

## Validated Lab Progression

| Lab | Capability                                                | Validation |
|-----|-----------------------------------------------------------|------------|
| 01  | TSO/E logon, ISPF, native READY and LOGOFF                | VALIDATED  |
| 02  | ISPF hierarchy, direct navigation, jump and RETURN        | VALIDATED  |
| 03  | SPLIT, SWAP and independent logical-screen state          | VALIDATED  |
| 04  | Data-set discovery, qualifiers and member-list processing | VALIDATED  |
| 05  | Read-only Browse navigation and positioning               | VALIDATED  |
| 06  | Browse representation, HEX and recursive inspection       | VALIDATED  |
| 07  | FIND, RFIND and targeted Browse search                    | VALIDATED  |
| 08  | Controlled Edit lifecycle, SAVE, CANCEL and restore       | VALIDATED  |
| 09  | Record insertion/deletion and rollback                    | VALIDATED  |
| 10  | Repeat, Copy, Move and destination semantics              | VALIDATED  |
| 11  | MASK, OVERLAY and column-position inspection              | VALIDATED  |
| 12  | BNDS, column shifting and data shifting                   | VALIDATED  |
| 13  | EXCLUDE, labels and TABS display state                    | VALIDATED  |
| 14  | Edit HEX, FIND, LOCATE and selective RESET                | VALIDATED  |
| 15  | Content/range EXCLUDE, DELETE, SORT and Recursive Edit    | VALIDATED  |

The detailed proof, commands, fixtures, negative tests and screenshots remain inside each lab.

## State, Mutation and Recovery

A central engineering theme of the Edit track is the distinction between
**display state**, **working data** and **persistent data**.

```text
Observe
   |
   v
Working session
   |
   +--> display-state change
   |
   +--> working-data mutation
             |
             +--> SAVE ------> persistent change
             |
             +--> CANCEL ----> baseline recovery
```

The repository does not treat a successful command as sufficient evidence. Where a lab changes data, the validation model can include baseline capture, controlled mutation, observed state transition, rollback, and independent post-recovery verification.

Labs 08–12 and 15 contain the strongest recovery-oriented evidence in the current track.

## Architecture V2

The repository participates in the portfolio lifecycle:

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

Not every lab exercises every lifecycle stage.

The maturity level attached to an individual lab applies only to the
**capability demonstrated by that lab**. It must not be interpreted as a
blanket maturity rating for the entire repository or the wider z/OS environment.

Examples already represented in the lab metadata include:

```text
M1 — Foundational
M2 — Operational
M3 — Resilient
```

The current labs remain primarily **I0 — Standalone** because they validate repository-owned interactive behavior without requiring a cross-repository execution path.

## Repository Boundary

A data set or member may be visible and editable through ISPF without transferring ownership of its technology to this repository.

For example:

```text
ISPF
  |
  +--> discover a JCL member
  +--> Browse a JCL member
  +--> Edit a JCL member
  |
  +--X JCL semantics
  +--X JES2 execution lifecycle
```

JCL semantics and JES2 processing belong to [`JCL_LABS`](https://github.com/P-dot/JCL_LABS).

The same ownership rule applies to REXX, USS, RACF, networking, COBOL, Db2, CICS, VSAM and other specialized domains.

## Cross-Domain Handoffs

The validated standalone capabilities in this repository are foundations for later portfolio integration.

```text
TSO/E / ISPF
     |
     +--> JCL_LABS
     |      JCL semantics / SUBMIT / JES2
     |
     +--> Rexx
     |      interactive automation / ISPF services
     |
     +--> UNIX_System_Services-
     |      USS operating environment
     |
     +--> application and data repositories
            editing / inspection as supporting operator capability
```

A handoff is not automatically evidence of cross-repository integration. Integration is marked validated only when the corresponding end-to-end path has actually been executed and documented.

## Evidence Standard

The repository follows an evidence-first method:

```text
BUILD / PREPARE
      |
      v
EXECUTE
      |
      v
OBSERVE
      |
      v
DIAGNOSE
      |
      v
CORRECT
      |
      v
VALIDATE
      |
      v
DOCUMENT
```

Depending on the capability, evidence can include:

- deterministic repository-owned fixtures;
- command transcripts;
- before/after record counts;
- expected and unexpected panel behavior;
- negative or protective behavior;
- rollback through `CANCEL`;
- independent final-state verification;
- screenshots from the tested z/OS environment;
- Architecture V2 metadata and validation notes.

No batch return code is invented for an interactive-only lab.

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
|   +-- 01-tso-e-logon-ready-ispf-environment/
|   +-- 02-ispf-navigation-hierarchy-direct-options-return/
|   +-- 03-ispf-split-screen-swap-logical-screens/
|   +-- 04-ispf-dataset-names-member-lists/
|   +-- 05-ispf-browse-navigation-scrolling-locate-labels/
|   +-- 06-ispf-browse-display-hex-recursive/
|   +-- 07-ispf-browse-find-rfind-search-controls/
|   +-- 08-ispf-edit-controlled-save-cancel-restore/
|   +-- 09-ispf-edit-insert-delete-line-commands/
|   +-- 10-ispf-edit-repeat-copy-move-before-after/
|   +-- 11-ispf-edit-mask-overlay-cols/
|   +-- 12-ispf-edit-bnds-column-data-shifting/
|   +-- 13-ispf-edit-exclude-labels-tabs/
|   +-- 14-ispf-edit-primary-commands/
|   +-- 15-ispf-edit-advanced-primary-commands/
|
+-- references/
```

## Current Boundary and Next Capability

Validated through:

```text
Lab 15
ISPF Edit Advanced Primary Commands
EXCLUDE / DELETE / SORT / Recursive Edit
```

Next:

```text
CHANGE
```

`CHANGE` is **NEXT**, not validated by the current repository state.

Broader cross-domain execution remains separate from this standalone capability progression and must be proven in the repository that owns the integration path.

## Security and Publication Standard

Before publication, evidence is reviewed to avoid exposing unnecessary operational or host-specific information, including:

- credentials, passwords, tokens and keys;
- private IP addresses;
- MAC addresses;
- host adapter identifiers;
- sensitive host/network configuration;
- unnecessary session identifiers or other environment-specific data.

Technical evidence should remain sufficient to reproduce and understand the engineering result without publishing unrelated sensitive information.

## Continue Through the Portfolio

This repository establishes the interactive operating foundation.

A natural portfolio progression is:

```text
MVS_TSO_ISPF
      |
      v
JCL_LABS
      |
      v
zos-batch-scheduler
      |
      v
Rexx / USS
      |
      v
application, data, security and integration tracks
```

Return to the [P-dot IBM z/OS engineering portfolio](https://github.com/P-dot).
