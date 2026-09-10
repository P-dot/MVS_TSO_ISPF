# Security Review — Lab 04

## Scope

This review covers the evidence selected for public publication in Lab 04.

## Evidence selection

The package contains only the screens needed to prove:

- the TSO prefix;
- DSLIST data-set discovery;
- selection of `IBMUSER.JCL.LAB`;
- member-list operations;
- member-pattern processing.

Full TSO/E logon and credential screens are not included.

## Review result

The selected screenshots contain:

- the lab user ID `IBMUSER`;
- the generic ADCD system context;
- ISPF panel and data-set names;
- member names and timestamps.

The selected screenshots do not contain:

- passwords;
- the ADCD default credential table;
- private IP addresses;
- MAC addresses;
- VTAM terminal identifiers;
- host network adapter information;
- host-side private network configuration.

## Content boundary

The evidence includes JCL source when Browse opens selected members. This is lab-owned source content used only to prove member selection; no credentials or private network values are present in the selected views.

## Text scan

The package text files were scanned for common private IPv4 and MAC-address patterns before ZIP creation.

## Publication decision

**Approved for repository publication.**
