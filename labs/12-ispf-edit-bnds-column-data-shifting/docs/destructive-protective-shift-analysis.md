# Destructive and Protective Shift Analysis

## Destructive column shift

Target:

```text
LEFT0005|AAA BBB CCC|RIGHT05
```

A right column shift was executed within restrictive bounds.

Observed:

- significant characters reached/crossed the right bound;
- trailing data was discarded in the Edit working state;
- data outside the bounds stayed in place.

This was intentional and remained uncommitted.

Recovery:

```text
CANCEL
```

restored the canonical member state.

## Protected data shift

Target:

```text
LEFT0006|  JJJ KKK  |RIGHT06
```

Command:

```text
<99
```

Observed:

```text
Data shifting incomplete
==ERR>
```

The editor preserved the significant data and moved it only as far as the configured boundary allowed.

`RESET` cleared the error marker/state.

## Engineering result

```text
column shift:
can be destructive at bounds

data shift:
protects significant data when requested movement cannot complete
```

Both paths were validated and recovered.
