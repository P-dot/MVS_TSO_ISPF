# References

## Primary source

- Kurt Bosler, *MVS TSO/ISPF: A Guide for Users and Developers*.

## Complementary sources

- Franz Lanz, *IBM z/OS ISPF Smart Practices, Volume 1: User's Guide*.
- Franz Lanz, *IBM z/OS ISPF Smart Practices, Volume 2: ISPF Programmer's Guide*.
- IBM Redbooks, *Introduction to the New Mainframe: z/OS Basics*.

## Lab 14 source mapping

Bosler Chapter 16 — *Edit Primary Commands*:

- HEX
- FIND
- LOCATE
- RESET
- SUBMIT

`SUBMIT` execution remains deferred to cross-repository ISPF -> JCL -> JES2 integration.

## Lab 15 source mapping

Bosler Chapter 17 — *Advanced Edit Primary Commands*:

- EXCLUDE
- DELETE
- SORT
- Recursive Edit

Lab 15 validates content-driven and range-driven exclusion, destructive DELETE with rollback, scoped SORT with rollback, and nested Edit context/return.
