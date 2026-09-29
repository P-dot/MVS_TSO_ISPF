# Architecture V2 Relationship

## Capability ownership

```text
Repository: MVS_TSO_ISPF
Domain: Operations and Service Management
Capability: interactive Edit display/search/positioning/state reset
```

## Why SUBMIT is deferred

The ISPF side owns the interactive primary command.

Actual job processing requires:

```text
ISPF Edit
   |
   v
SUBMIT
   |
   v
JCL
   |
   v
JES2
```

The JCL and JES2 layers are separate validated domains/repositories.

Lab 14 therefore stops at the repository boundary rather than duplicating JCL or JES2 curriculum.

## Integration target

A later Production Track should consume already validated capabilities from each repository and prove the complete submission lifecycle.
