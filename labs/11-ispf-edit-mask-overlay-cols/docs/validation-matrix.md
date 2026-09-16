# Validation Matrix — Lab 11

| Test | Expected | Observed | Status |
|---|---|---|---|
| Baseline | 12 records | 12 records | PASS |
| Initial MASK | profile state captured | blank mask observed | PASS |
| Configure MASK | template retained | template displayed and reused | PASS |
| I3 with MASK | three preformatted inputs | three generated | PASS |
| Unused masked input | unused line disappears | only two populated rows remained | PASS |
| Hide MASK | mask line hidden only | subsequent INSERT still inherited mask | PASS |
| Redisplay MASK | same stored template returns | retained value observed | PASS |
| MASK profile rollback | blank restored | blank mask revalidated | PASS |
| Data rollback after MASK | baseline 12 | independent Browse = 12 | PASS |
| C + O | target merged, source preserved | target received suffix; source retained | PASS |
| CC/OO block overlay | ordered block merge | A->A and B->B observed | PASS |
| MOVE + O protection | incomplete placement must not delete source | `Line not deleted` observed; source retained | PASS |
| COLS display | indicator appears before selected line | observed | PASS |
| Multiple COLS | more than one indicator can coexist | two indicators observed | PASS |
| Delete one COLS | special line removed, data preserved | observed | PASS |
| Final rollback | persistent state baseline | independent Browse = 12 | PASS |

## Final decision

**VALIDATED — M3 Resilient**

M3 is supported by profile-state restoration, repeated data rollback, a real protected MOVE/OVERLAY condition, and independent post-recovery verification.
