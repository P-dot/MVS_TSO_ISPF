# Source and Scope Mapping — Lab 15

## Bosler Chapter 17

```text
Advanced Edit Primary Commands

- EXCLUDE
- DELETE
- SORT
- Recursive Edit
```

## Executed

```text
content-driven EXCLUDE
label-range EXCLUDE
DELETE ALL X
SORT by columns and label range
Recursive Edit to same-PDS member
return to parent Edit session
```

## Scope boundary

The lab does not move into Chapter 18 `CHANGE`.

## Environment-specific observation

The tested ISPF environment required:

```text
EXCLUDE ALL .XA .XB
```

for full label-range exclusion.

The shorter:

```text
EXCLUDE .XA .XB
```

was interpreted as a string-oriented form and produced `Put string in quotes`.
