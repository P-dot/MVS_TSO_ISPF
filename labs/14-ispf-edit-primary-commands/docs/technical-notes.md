# Technical Notes — Lab 14

## HEX

`HEX ON` exposed the hexadecimal representation of each record.

`HEX ON DATA` changed the hexadecimal presentation mode.

`HEX OFF` restored the ordinary character representation.

No data bytes were modified.

## FIND with X and NX

A six-record block was excluded.

`F ALL COUNT X` operated on excluded lines and redisplayed the three records containing `COUNT`.

`F DO NX` then searched the visible/non-excluded set only. It found the visible record containing both `COUNT` and `DO` while the separately excluded `FILTER-04 DO GAMMA` remained outside that search scope.

## FIND with BNDS

Restrictive bounds were configured at columns 11–16.

The fixture deliberately placed one `TARGET` occurrence inside those bounds and one at columns 1–6.

`F TARGET` found the bounded occurrence and ignored the left-side occurrence.

## LOCATE and state classes

`LOCATE` was validated against:

```text
line number
.ZFIRST
.ZLAST
COMMAND
SPECIAL
EXCLUDED
```

## Selective RESET

Three independent states existed simultaneously:

```text
pending command
special display lines
excluded records
```

Each was cleared with its corresponding RESET operand while the other state classes remained intact.

## Expected pending-command diagnostic

A deliberately incomplete `CC` block generated:

```text
Block command incomplete
```

This is recorded as expected evidence of a pending block command, not as a lab failure.

## SUBMIT boundary

Chapter 16 introduces `SUBMIT`, but actual execution crosses from interactive ISPF ownership into JCL/JES2 processing.

Therefore this lab documents the command but deliberately defers execution to a later cross-repository integration scenario.
