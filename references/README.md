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

This lab executes the repository-owned interactive capabilities:

```text
HEX
FIND
LOCATE
RESET
```

`SUBMIT` is documented as an integration boundary and deferred to a cross-repository ISPF -> JCL -> JES2 workflow.
