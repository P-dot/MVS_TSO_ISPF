# State and Boundary Model — Lab 12

## Two state domains

```text
DATA STATE
IBMUSER.ISPF.LAB(EDIT12)

PROFILE STATE
BNDS
```

Both are restored before closure.

## Safe column shifting

```text
known baseline
   |
restrictive BNDS
   |
safe )2 / (
   |
outside-bound text preserved
   |
CANCEL
   |
baseline restored
```

## Destructive column shifting

```text
full bounded field
   |
)2
   |
significant characters cross right bound
   |
working-state truncation
   |
CANCEL
   |
canonical record restored
```

## Protected data shifting

```text
<99
   |
requested displacement exceeds free space
   |
editor shifts only as far as safe
   |
Data shifting incomplete
==ERR>
   |
RESET
   |
error display cleared
```

## Final invariant

```text
persistent_record_count == 11
persistent_content == fixtures/edit/EDIT12-baseline.txt
BNDS == pre-lab/default state
```
