# References

The project uses documentation as the primary learning source; no video course is used as the lab sequence.

## Primary source

- Kurt Bosler, *MVS TSO/ISPF: A Guide for Users and Developers*, McGraw-Hill / J. Ranade IBM Series.

## Complementary sources

- Franz Lanz, *IBM z/OS ISPF Smart Practices, Volume 1: User's Guide*, De Gruyter, 2015.
- Franz Lanz, *IBM z/OS ISPF Smart Practices, Volume 2: ISPF Programmer's Guide*, De Gruyter, 2015.
- IBM Redbooks, *Introduction to the New Mainframe: z/OS Basics*, SG24-6366-00.
- IBM Redbooks, *z/OS Version 1 Release 11 Implementation*, SG24-7729-00.

## Lab 11 source mapping

Lab 11 follows Bosler Chapter 13, *Advanced Edit Line Commands: Section 1*.

Validated topics:

- `MASK` display and profile-backed mask state;
- templated INSERT behavior;
- unused masked input line removal;
- hidden mask remaining effective;
- explicit restoration of the mask profile to blank;
- `OVERLAY` as a line merge using `COPY`/`MOVE`;
- block overlay using `CC`/`OO`;
- protected `MOVE + OVERLAY` with `Line not deleted`;
- `COLS` as an Edit line command;
- multiple simultaneous column-indicator lines;
- deletion of a column indicator without affecting real data;
- final rollback to the canonical 12-record fixture.

Lab 11 deliberately stops before Bosler Chapter 14 topics: `BNDS` and column/data shifting.

The source publications themselves are **not redistributed in this repository**.
