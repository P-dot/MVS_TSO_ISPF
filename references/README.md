# References

The project uses documentation as the primary learning source; no video course is used as the lab sequence.

## Primary source

- Kurt Bosler, *MVS TSO/ISPF: A Guide for Users and Developers*, McGraw-Hill / J. Ranade IBM Series.

## ISPF complementary sources

- Franz Lanz, *IBM z/OS ISPF Smart Practices, Volume 1: User's Guide*, De Gruyter, 2015.
- Franz Lanz, *IBM z/OS ISPF Smart Practices, Volume 2: ISPF Programmer's Guide*, De Gruyter, 2015.

## IBM complementary sources

- IBM Redbooks, *Introduction to the New Mainframe: z/OS Basics*, SG24-6366-00.
- IBM Redbooks, *z/OS Version 1 Release 11 Implementation*, SG24-7729-00.

## Lab 09 source mapping

Lab 09 follows Bosler Chapter 11, *Basic Edit Line Commands: Section 1*, covering INSERT and DELETE forms and pending block-command recovery.

## Lab 10 source mapping

Lab 10 follows Bosler Chapter 12, *Basic Edit Line Commands: Section 2*.

Validated topics:

- `R`, `R3`, and `RR`/`RR`;
- `A` and `B` as destination controls;
- `C`, `C2`, and `CC`/`CC`;
- `M`, `M2`, and `MM`/`MM`;
- numeric destination repetition with `A2`;
- `MOVE/COPY is pending`;
- multiple line commands;
- controlled `Command conflict` negative test;
- corrected non-conflicting multiple-command execution;
- `CANCEL` rollback and independent Browse verification after each transaction.

IBM Redbooks is used as complementary confirmation of standard ISPF Edit line-command semantics.

Lab 10 deliberately stops before Bosler Chapter 13 topics: `MASK` and `OVERLAY`.

The source publications themselves are **not redistributed in this repository**.
