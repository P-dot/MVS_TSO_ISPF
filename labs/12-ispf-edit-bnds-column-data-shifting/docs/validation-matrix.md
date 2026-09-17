# Validation Matrix — Lab 12

| Test | Expected | Observed | Status |
|---|---|---|---|
| Fixture baseline | 11 records | 11 records | PASS |
| COLS | column ruler displayed | observed | PASS |
| BNDS baseline | original/default bounds captured | observed | PASS |
| Restrictive BNDS | bounded test region configured | observed | PASS |
| Safe right column shift | data moves right inside BNDS | observed | PASS |
| Safe left column shift | default two-column shift | observed | PASS |
| Outside-bound protection | LEFT/RIGHT text stays fixed | observed | PASS |
| Safe-shift rollback | baseline restored | observed after CANCEL | PASS |
| Destructive column shift | trailing data can be lost at bound | working-state truncation observed | PASS |
| Destructive-shift rollback | original record recovered | observed | PASS |
| Excessive data shift `<99` | preserve significant data, stop at bound | observed | PASS |
| Incomplete data shift | diagnostic emitted | `Data shifting incomplete` | PASS |
| Error marker | line marked | `==ERR>` | PASS |
| RESET | error display cleared | observed | PASS |
| Block `>>2` | two-line block shifts right | observed | PASS |
| BNDS profile restoration | original/default bounds restored | observed | PASS |
| Final post-recovery state | canonical 11 records | independent Browse = 11 | PASS |

## Final decision

**VALIDATED — M3 Resilient**

M3 is supported by a deliberately destructive working-state test, explicit recovery, a protected incomplete data-shift condition, RESET recovery, BNDS profile restoration and independent final Browse validation.
