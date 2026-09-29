# Pull Request Validation Notes — Lab 14

## Objective

Add Lab 14 validating ISPF Edit primary commands while preserving Architecture V2 repository boundaries.

## Architecture V2

```text
Domain: Operations and Service Management
Capability: Controlled ISPF Edit display, search, positioning and selective session-state reset
Lifecycle: Baseline / Configure / Operate / Observe
Maturity: M2 — Operational
Integration level: I0 — Standalone
Validation status: VALIDATED
```

## Validation

- HEX ON / HEX ON DATA / HEX OFF
- FIND against excluded and non-excluded line sets
- FIND constrained by BNDS
- LOCATE by line number and built-in labels
- LOCATE by COMMAND / SPECIAL / EXCLUDED state classes
- RESET COMMAND / SPECIAL / EXCLUDED isolation
- BNDS profile restoration
- independent final Browse
- SUBMIT boundary documented and deferred

## Final state

```text
final persistent record count: 18
persistent state: BASELINE UNCHANGED
BNDS state: DEFAULT RESTORED
SUBMIT: DEFERRED TO CROSS-REPOSITORY INTEGRATION
```
