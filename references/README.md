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

Lab 09 follows Bosler Chapter 11, *Basic Edit Line Commands: Section 1*.

Validated topics:

- line-command area and Enter-driven execution;
- `I` single-line insertion;
- `I3` multiple-line insertion;
- `D` single-line deletion;
- `D3` count-based deletion;
- `DD` / `DD` block deletion;
- pending block-command state;
- `RESET` clearing an incomplete block line command.

IBM Redbooks is used as a complementary source for the standard `I`, `In`, `D`, `Dn`, and block line-command model.

Lab 09 deliberately stops before Bosler Chapter 12 topics: Repeat, Before/After, Copy and Move.

The source publications themselves are **not redistributed in this repository**.
