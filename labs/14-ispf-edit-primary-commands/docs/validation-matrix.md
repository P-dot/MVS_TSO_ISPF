# Validation Matrix — Lab 14

| Capability | Expected | Observed | Status |
|---|---|---|---|
| Baseline | 18 canonical records | 18 records | PASS |
| HEX ON | vertical hexadecimal display | observed | PASS |
| HEX ON DATA | DATA hexadecimal display | observed | PASS |
| HEX OFF | normal character display | restored | PASS |
| block EXCLUDE | six FILTER lines excluded | 6 lines hidden | PASS |
| `F ALL COUNT X` | search excluded lines | three COUNT lines redisplayed | PASS |
| `F DO NX` | search visible/non-excluded set | FILTER-03 found; excluded FILTER-04 ignored | PASS |
| `RESET EXCLUDED` | restore excluded FILTER lines | full block restored | PASS |
| BNDS 11–16 | restrict FIND scope | configured | PASS |
| `F TARGET` | find occurrence inside current bounds only | inside occurrence found; left-side occurrence ignored | PASS |
| `L 15` | position line 15 | LOCATE-LINE-A positioned | PASS |
| `L .ZLAST` | position last record | ISPF-LAB14-END positioned | PASS |
| `L .ZFIRST` | position first record | baseline first record positioned | PASS |
| pending block command | establish command state | `CC` pending / Block command incomplete | PASS |
| `L COMMAND` | locate pending command | observed | PASS |
| `RESET COMMAND` | clear command state only | command cleared; other states preserved | PASS |
| `L SPECIAL` | locate special state | observed | PASS |
| `RESET SPECIAL` | clear special display only | special lines removed; excluded state preserved | PASS |
| `L EXCLUDED` | locate excluded state | observed | PASS |
| `RESET EXCLUDED` | redisplay excluded records | records restored | PASS |
| BNDS restoration | return profile to default bounds | left=1; restricted right bound removed | PASS |
| final Browse | persistent data unchanged | 18 canonical records | PASS |
| SUBMIT | respect repository boundary | execution deferred | PASS / DEFERRED |

## Final decision

**VALIDATED — M2 Operational**

The lab demonstrates repeatable operation and observation of Edit primary-command behavior and selective state cleanup. No artificial failure/recovery cycle was introduced, so M2 is retained.
