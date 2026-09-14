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

## Lab 05 source mapping

Lab 05 is based mainly on:

- Bosler, Chapter 7, *The Browse Function*: scrolling, terminating Browse, `LOCATE`, line-number positioning, label assignment and label location.
- Lanz, Volume 1, as complementary context for ISPF Browse usage and data-set/member interaction.

## Lab 06 source mapping

Lab 06 is based mainly on:

- Bosler, Chapter 8, *Browse Commands*: `COLUMNS`, `RESET`, `DISPLAY`, `HEX` and Recursive Browse.
- Bosler's documented hexadecimal display modes `HEX ON VERT`, `HEX ON DATA` and `HEX OFF`.
- Bosler's description of Recursive Browse, where the parent Browse session is suspended while another member is browsed.
- IBM z/OS 1.11 / ISPF 6.1 behavior as directly observed in this laboratory.

## Lab 07 source mapping

Lab 07 is based mainly on:

- Bosler, Chapter 9, *The Browse FIND Command*: basic `FIND`, repeat find (`RFIND`), case handling, search direction, context, column restrictions, hexadecimal strings and picture strings.
- Bosler's FIND syntax summary, including `NEXT`, `PREV`, `FIRST`, `LAST`, `ALL`, `CHARS`, `PREFIX`, `SUFFIX` and `WORD`.
- Bosler's distinction between normal text strings and case-sensitive character strings.
- IBM z/OS 1.11 / ISPF 6.1 behavior as directly observed in this laboratory.

## Lab 08 source mapping

Lab 08 begins the Edit capability block and is based mainly on:

- Bosler, Chapter 10, *The Edit Function*: entering Edit, creating a member and modifying existing data.
- Bosler's Edit data-storage behavior for explicit `SAVE` and `CANCEL`.
- Lanz, Volume 1, Chapter 8, for `PROFILE 9`, Edit Profile characteristics, `RECOVERY`, `AUTOSAVE`, `STATS`, and UNDO prerequisites.
- IBM Redbooks, *Introduction to the New Mainframe: z/OS Basics*, Edit discussion distinguishing primary commands, line commands and text overtype, and documenting `SAVE`/PF3 versus `CANCEL`.
- Directly observed IBM z/OS 1.11 / ISPF 6.1 behavior from the laboratory.

Lab 08 deliberately limits its mutation scope to direct text overtype plus explicit persistence/rollback. Insert/delete/copy/move line-command semantics remain the next capability.

Other IBM manuals are added only when a lab requires them.

The source publications themselves are **not redistributed in this repository**.
