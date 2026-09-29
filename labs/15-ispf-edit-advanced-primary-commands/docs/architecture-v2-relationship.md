# Architecture V2 Relationship

## Ownership

```text
Domain:
Operations and Service Management

Repository:
MVS_TSO_ISPF

Capability:
content-driven selection
scoped mutation
resequencing
nested Edit context
```

All tested behaviors remain native interactive ISPF capabilities, so the lab remains:

```text
I0 — Standalone
```

No cross-repository execution is required.

## Capability evolution

```text
Lab 13
display-state exclusion / labels

Lab 14
primary command search / locate / selective reset

Lab 15
primary EXCLUDE
destructive DELETE + rollback
SORT + rollback
Recursive Edit
```

## Next capability

Bosler Chapter 18 moves from selection/resequencing to controlled content transformation with the `CHANGE` primary command.
