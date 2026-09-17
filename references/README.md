# References

## Primary source

- Kurt Bosler, *MVS TSO/ISPF: A Guide for Users and Developers*, McGraw-Hill / J. Ranade IBM Series.

## Complementary sources

- Franz Lanz, *IBM z/OS ISPF Smart Practices, Volume 1: User's Guide*, De Gruyter, 2015.
- Franz Lanz, *IBM z/OS ISPF Smart Practices, Volume 2: ISPF Programmer's Guide*, De Gruyter, 2015.
- IBM Redbooks, *Introduction to the New Mainframe: z/OS Basics*, SG24-6366-00.
- IBM Redbooks, *z/OS Version 1 Release 11 Implementation*, SG24-7729-00.

## Lab 12 source mapping

Lab 12 follows Bosler Chapter 14, *Advanced Edit Line Commands: Section 2*:

- `BNDS` line command;
- Column Shifting;
- Data Shifting.

The lab validates:

- current/default bounds observation;
- controlled restrictive bounds;
- safe left/right column shifts;
- destructive column shifting at a right boundary;
- rollback after destructive working-state modification;
- data shifting with an intentionally excessive shift request;
- `Data shifting incomplete`;
- `==ERR>` handling;
- `RESET`;
- block data shifting;
- restoration of the original/default bounds;
- independent final Browse verification.

Lab 12 deliberately stops before Bosler Chapter 15:

- EXCLUDE line command;
- Edit Labels;
- TABS line command.

The source publications themselves are **not redistributed in this repository**.
