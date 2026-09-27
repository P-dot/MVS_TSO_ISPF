# Pull Request Validation Notes — Lab 13

## Objective

Add Lab 13 validating selective ISPF Edit visibility, Edit labels and TABS special-line display state.

## Architecture V2

```text
Domain: Operations and Service Management
Capability: Selective ISPF Edit visibility, session-scoped positioning and special-line state inspection
Lifecycle: Baseline / Operate / Observe
Maturity: M2 — Operational
Integration level: I0 — Standalone
Validation status: VALIDATED
```

## Validation performed

- canonical 18-record fixture established;
- single-line EXCLUDE with `X`;
- numeric EXCLUDE with `X3`;
- first/last partial redisplay with `F` and `L`;
- block EXCLUDE with `XX/XX`;
- indentation-aware `S2` observation;
- user-defined Edit labels;
- LOCATE to `.MID`;
- built-in `.ZLAST` and `.ZFIRST`;
- selective label cleanup with `RESET LABEL`;
- `TABS` special-line display;
- special-line cleanup with `RESET SPECIAL`;
- independent final Browse.

## Result

```text
X: PASS
X3: PASS
F: PASS
L: PASS
XX/XX: PASS
S2: PASS
indentation semantics: OBSERVED
custom labels: PASS
L .MID: PASS
L .ZLAST: PASS
L .ZFIRST: PASS
RESET LABEL: PASS
=TABS>: PASS
RESET SPECIAL: PASS
final persistent record count: 18
final state: BASELINE UNCHANGED
```

## Maturity decision

M2 is retained deliberately. The lab validates normal operational/session-state behavior and does not claim an artificial failure/recovery cycle.

## Next capability

Bosler Chapter 16 — Edit Primary Commands:

```text
HEX / FIND / LOCATE / RESET / SUBMIT
```
