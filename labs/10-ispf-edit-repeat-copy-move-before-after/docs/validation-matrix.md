# Validation Matrix — Lab 10

| Test | Expected | Observed | Status |
|---|---|---|---|
| Baseline | 28 records | 28 records | PASS |
| `R` | +1 | 28 -> 29 | PASS |
| `R3` | +3 additional copies | 29 -> 32 | PASS |
| `RR/RR` | duplicate 2-record block preserving order | 32 -> 34 | PASS |
| REPEAT rollback | persistent state returns to 28 | independent Browse = 28 | PASS |
| `C + A` | source retained, one copy after target | 28 -> 29 | PASS |
| `C2 + B` | two source lines copied before target | 29 -> 31 | PASS |
| `CC/CC + A` | block copied after target | 31 -> 33 | PASS |
| pending COPY/MOVE | operation waits for completion | `MOVE/COPY is pending` observed | PASS |
| COPY rollback | persistent state returns to 28 | independent Browse = 28 | PASS |
| `M + B` | relocate one record, count unchanged | 28 -> 28 | PASS |
| `M2 + A2` | 2-record payload relocated and repeated twice | 28 -> 30 | PASS |
| `MM/MM + B` | block relocated, count unchanged | 30 -> 30 | PASS |
| MOVE rollback | persistent state returns to 28 | independent Browse = 28 | PASS |
| conflicting multiple set | conflict must not silently mutate data | `Command conflict` observed | PASS |
| conflict recovery | CANCEL + Browse restores baseline | 28 records | PASS |
| corrected multiple set | `R` + `C/A` in one Enter | 28 -> 30 | PASS |
| final rollback | persistent state returns to baseline | 28 records | PASS |

## Final decision

**VALIDATED — M3 Resilient**

M3 is evidence-driven. The lab includes a real command-conflict condition, controlled recovery, corrected execution, and independent post-recovery verification.
