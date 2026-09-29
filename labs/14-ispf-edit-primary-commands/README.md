# Lab 14 — ISPF Edit Primary Commands: HEX, FIND, LOCATE and RESET

## Architecture metadata

```yaml
architecture:
  domain: "Operations and Service Management"
  capability: "Controlled ISPF Edit display, search, positioning and selective session-state reset"
  lifecycle:
    - Baseline
    - Configure
    - Operate
    - Observe
  maturity: "M2 — Operational"
  integration_level: "I0 — Standalone"
```

## Objective

Validate Bosler Chapter 16 primary-command behavior that is owned directly by the ISPF repository while explicitly preserving the Architecture V2 boundary around `SUBMIT`.

## Fixture

```text
IBMUSER.ISPF.LAB(EDIT14)
```

Canonical fixture:

```text
fixtures/edit/EDIT14-baseline.txt
```

Baseline:

```text
18 records
```

## HEX

Validated:

```text
HEX ON
HEX ON DATA
HEX OFF
```

The representation changed while persistent data remained untouched.

## FIND over excluded and visible sets

A six-line FILTER block was excluded.

```text
F ALL COUNT X
```

redisplayed the three excluded records containing `COUNT`.

```text
F DO NX
```

then searched only the visible/non-excluded set.

The visible `FILTER-03 COUNT DO BETA` was found, while excluded `FILTER-04 DO GAMMA` remained outside scope.

## FIND constrained by BNDS

Restrictive bounds:

```text
11–16
```

were configured.

The fixture contains:

```text
BOUNDS-IN|TARGET|RIGHT
TARGET-OUTSIDE-LEFT
```

`F TARGET` found the occurrence in columns 11–16 and ignored the occurrence in columns 1–6.

## LOCATE

Validated:

```text
L 15
L .ZLAST
L .ZFIRST
L COMMAND
L SPECIAL
L EXCLUDED
```

## Selective RESET

Three simultaneous states were created:

```text
COMMAND
SPECIAL
EXCLUDED
```

Then independently cleared:

```text
RESET COMMAND
RESET SPECIAL
RESET EXCLUDED
```

Each reset preserved the other state classes until their own selective reset was executed.

## Expected diagnostic

A deliberately incomplete block-copy command produced:

```text
Block command incomplete
```

This was expected evidence of pending COMMAND state.

## BNDS profile restoration

The restrictive bounds were removed.

Final profile state returned to:

```text
left boundary = 1
right boundary = default
```

## Final validation

After cleanup:

```text
CANCEL
B EDIT14
```

showed exactly the 18 canonical records.

```text
persistent state = BASELINE UNCHANGED
```

## SUBMIT boundary

Bosler Chapter 16 also introduces `SUBMIT`.

Execution is intentionally deferred:

```text
ISPF
  -> SUBMIT
  -> JCL
  -> JES2
```

The complete submission lifecycle belongs to a later cross-repository integration scenario.

## Final classification

```text
VALIDATED
M2 — Operational
I0 — Standalone
```

## Next capability

**Bosler Chapter 17 — Advanced Edit Primary Commands**
