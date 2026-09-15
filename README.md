# MVS TSO/ISPF Labs

Hands-on TSO/E and ISPF laboratories executed on an IBM z/OS 1.11 ADCD environment.

The lab sequence is documentation-led. The main historical/didactic source is Kurt Bosler's *MVS TSO/ISPF: A Guide for Users and Developers*, complemented by Franz Lanz's *IBM z/OS ISPF Smart Practices* and IBM z/OS documentation.

## Labs

| Lab | Topic | Status |
|---|---|---|
| [01](labs/01-tso-e-logon-ready-ispf-environment/) | TSO/E logon, native READY mode and ISPF environment | ✅ Completed |
| [02](labs/02-ispf-navigation-hierarchy-direct-options-return/) | ISPF hierarchy, direct option entry, jump function and RETURN | ✅ Completed |
| [03](labs/03-ispf-split-screen-swap-logical-screens/) | ISPF logical screens, SPLIT, SWAP and task-list validation | ✅ Completed |
| [04](labs/04-ispf-dataset-names-member-lists/) | Data set naming, DSLIST and member-list processing | ✅ Completed |
| [05](labs/05-ispf-browse-navigation-scrolling-locate-labels/) | ISPF Browse navigation, scrolling, LOCATE and labels | ✅ Completed |
| [06](labs/06-ispf-browse-display-hex-recursive/) | ISPF Browse display controls, hexadecimal representation and recursive Browse | ✅ Completed |
| [07](labs/07-ispf-browse-find-rfind-search-controls/) | ISPF Browse FIND, RFIND and search controls | ✅ Completed |
| [08](labs/08-ispf-edit-controlled-save-cancel-restore/) | Controlled ISPF Edit lifecycle: SAVE, CANCEL, persistence and restore | ✅ Completed |
| [09](labs/09-ispf-edit-insert-delete-line-commands/) | ISPF Edit line commands: controlled INSERT and DELETE | ✅ Completed |

## Method

Each lab records Architecture V2 metadata, objective, engineering context, scope, exact interactive flow, commands, expected and observed results, evidence, failure/recovery behavior, security review and source references.

Architecture V2 classifies new work by engineering domain, capability, lifecycle stage, maturity level and integration level while preserving the historical lab sequence.

## Environment

- IBM z/OS 1.11 ADCD
- TSO/E
- ISPF 6.1 (observed in the labs)
- 3270/TN3270 interactive access

## Ecosystem role

This repository owns the interactive TSO/E and ISPF foundation of the wider z/OS engineering laboratory. It provides the operator-facing base later consumed by JCL, REXX, scheduler tooling and other specialized repositories.

See [MVS TSO/ISPF Ecosystem Integration](docs/ECOSYSTEM-INTEGRATION.md).

## Repository-owned Edit fixtures

State-changing ISPF labs use repository-owned fixtures rather than modifying artifacts owned by JCL, COBOL, REXX or other specialized repositories.

```text
IBMUSER.ISPF.LAB
        |
        +--> EDIT08
        +--> EDIT09
        +--> future Edit fixtures
```

Canonical baselines are preserved under `fixtures/edit/`.

## Architecture V2 progression

```text
TSO/E logon
  -> ISPF navigation
  -> dataset/member work
  -> Browse navigation / representation / search
  -> controlled Edit lifecycle
  -> Edit INSERT / DELETE line commands
  -> Repeat / Copy / Move / Before / After
  -> advanced Edit / utilities
  -> REXX / ISPF automation prerequisites
```

## Publication security

Evidence is reviewed before publication. Credentials, IP addresses, MAC addresses, terminal/network identifiers and host-side network details are not intentionally published.
