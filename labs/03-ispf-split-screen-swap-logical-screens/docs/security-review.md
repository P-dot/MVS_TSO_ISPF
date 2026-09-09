# Security Review — Lab 03

## Scope

This review covers the evidence selected for public publication in Lab 03.

## Evidence selection

Only ISPF panels required to prove logical-screen creation, switching, enumeration and closure were selected.

The TSO/E logon sequence and ADCD credential information are not included.

## Review result

The selected screenshots contain:

- ISPF menus and panels;
- the generic lab user ID `IBMUSER`;
- the generic ADCD system identifier;
- ISPF panel IDs and application IDs;
- logical-screen numbers;
- 3270 session type.

The selected screenshots do not contain:

- passwords;
- the ADCD default credential table;
- IP addresses;
- MAC addresses;
- terminal/network identifiers such as the initial VTAM terminal identifier;
- host network adapter information;
- host-side private network configuration.

## Text scan

The package text files were scanned for common private IPv4 and MAC-address patterns before creation of the ZIP archive.

## Publication decision

**Approved for repository publication.**
