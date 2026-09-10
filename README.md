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

## Method

Each lab records the objective, concepts, exact interactive flow, commands, observed results, evidence, security review and source references. Historical MVS material is validated against the behavior of the z/OS environment instead of being reproduced blindly.

## Environment

- IBM z/OS 1.11 ADCD
- TSO/E
- ISPF 6.1 (observed in the labs)
- 3270/TN3270 interactive access

## Ecosystem role

This repository owns the interactive TSO/E and ISPF foundation of the wider z/OS engineering laboratory. It provides the operator-facing base later consumed by JCL, REXX, scheduler tooling and other specialized repositories.

See [MVS TSO/ISPF Ecosystem Integration](docs/ECOSYSTEM-INTEGRATION.md).

## Publication security

Evidence is reviewed before publication. Credentials, IP addresses, MAC addresses, terminal/network identifiers and host-side network details are not intentionally published.
