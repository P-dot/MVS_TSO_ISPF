# Validation Matrix — Lab 13

| Capability | Expected | Observed | Status |
|---|---|---|---|
| Baseline | 18 canonical records | 18 records | PASS |
| `X` | hide one record without deleting it | 1 line not displayed | PASS |
| `RESET` after `X` | redisplay excluded record | full display restored | PASS |
| `X3` | hide three records starting at target | 3 lines not displayed | PASS |
| `F` | redisplay first excluded record | first record restored; 2 hidden remain | PASS |
| `L` | redisplay last excluded record | last record restored; 1 hidden remains | PASS |
| `XX/XX` | exclude contiguous block | 5-line block hidden | PASS |
| `S2` | redisplay by SHOW selection | ROOT and CHILD-A restored | PASS |
| SHOW indentation behavior | favor less-indented records | observed in fixture hierarchy | PASS |
| Custom labels | create session labels | `.START`, `.MID`, `.END` observed | PASS |
| `L .MID` | locate user label | LABEL-MIDDLE positioned | PASS |
| `L .ZLAST` | locate built-in last label | final record positioned | PASS |
| `L .ZFIRST` | locate built-in first label | first record positioned | PASS |
| `RESET LABEL` | clear custom labels | numeric line identifiers restored | PASS |
| `TABS` line command | show special tab-state line | `=TABS>` displayed | PASS |
| TABS scope boundary | no advanced tab configuration | no tab configuration modified | PASS |
| `RESET SPECIAL` | remove special line | `=TABS>` removed | PASS |
| Final Browse | persistent data unchanged | 18 canonical records | PASS |

## Final decision

**VALIDATED — M2 Operational**

The lab proves repeatable operation and observation of display/session state. No exceptional failure-and-recovery scenario was required or claimed, so the lab remains M2 rather than being artificially promoted to M3.
