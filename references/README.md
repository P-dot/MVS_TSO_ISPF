# References

The project uses documentation as the primary learning source; no video course is used as the lab sequence.

## Primary source

- Kurt Bosler, *MVS TSO/ISPF: A Guide for Users and Developers*, McGraw-Hill / J. Ranade IBM Series.

## ISPF complementary sources

- Franz Lanz, *IBM z/OS ISPF Smart Practices, Volume 1: User's Guide*, De Gruyter, 2015.
- Franz Lanz, *IBM z/OS ISPF Smart Practices, Volume 2: ISPF Programmer's Guide*, De Gruyter, 2015. Reserved mainly for later ISPF development/REXX labs.

## IBM complementary sources

- IBM Redbooks, *Introduction to the New Mainframe: z/OS Basics*, SG24-6366-00.
- IBM Redbooks, *z/OS Version 1 Release 11 Implementation*, SG24-7729-00.

## Lab 02 source mapping

Lab 02 is based mainly on:

- Bosler, Chapter 4, *Accessing ISPF*: ISPF hierarchy, option/suboption selection, direct option entry, jump function and RETURN/END navigation concepts.
- Lanz, Volume 1, Chapter 4, *Customize ISPF*: Primary Option Menu and practical handling of ISPF panels.
- IBM Redbooks, *Introduction to the New Mainframe: z/OS Basics*: practical use of direct ISPF paths such as `=3.4`.

## Lab 03 source mapping

Lab 03 is based mainly on:

- Bosler, Chapter 4, *Accessing ISPF*: split-screen operation and navigation between ISPF contexts.
- Lanz, Volume 1, section 4.7, *Screen splitting*, including logical-screen handling and direct activation concepts.
- IBM ISPF behavior validated directly in the z/OS 1.11 lab through `F2/SPLIT`, `F9/SWAP`, `SWAP LIST` and `F3/END`.

Other IBM manuals are added only when a lab requires them (JCL, REXX, VSAM, RACF, USS, and related components).

The source publications themselves are **not redistributed in this repository**.
