# Validation Matrix — Lab 15

| Capability | Expected | Observed | Status |
|---|---|---|---|
| EDIT15 baseline | 17 canonical records | 17 records | PASS |
| EDIT15R baseline | 3 canonical records | 3 records | PASS |
| `X ALL DROP` | exclude lines containing DROP | exactly two lines hidden | PASS |
| `RESET EXCLUDED` | redisplay DROP lines | full display restored | PASS |
| label setup | `.XA` / `.XB` delimit range | labels observed | PASS |
| `EXCLUDE .XA .XB` | test source-style shorthand | environment requested quoted string | OBSERVED |
| `EXCLUDE ALL .XA .XB` | exclude full label range | 4 lines hidden | PASS |
| `RESET LABEL` | clear user labels | numeric line numbers restored | PASS |
| `DEL ALL X` | delete excluded lines | `2 lines deleted` | PASS |
| destructive working state | record count reduced | 17 -> 15 | PASS |
| DELETE rollback | restore canonical fixture | CANCEL -> 17 records | PASS |
| SORT field | columns 6–7 | 03/01/04/02 identified | PASS |
| SORT label range | `.SA`–`.SB` only | controlled block sorted | PASS |
| SORT ascending | 03/01/04/02 -> 01/02/03/04 | observed | PASS |
| SORT rollback | restore original order | CANCEL restored 03/01/04/02 | PASS |
| Recursive Edit | parent opens child member | EDIT15R active | PASS |
| child fixture | 3 expected records | observed | PASS |
| child CANCEL | resume parent session | EDIT15 active again | PASS |

## Final decision

**VALIDATED — M3 Resilient**

M3 is evidence-based: the lab includes destructive working-state deletion and resequencing, both followed by controlled rollback, plus verified parent/child Edit context recovery.
