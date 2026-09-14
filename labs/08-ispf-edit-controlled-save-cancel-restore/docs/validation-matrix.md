# Validation Matrix — Lab 08

| Test | Expected result | Observed result | Status |
|---|---|---|---|
| PDS allocation | `IBMUSER.ISPF.LAB` available as FB80 PDS fixture library | Allocation panel completed with PDS / FB / LRECL 80 / BLKSIZE 0 / TRACK 1,1 / directory 10 | PASS |
| Initial member creation | `EDIT08` can be created and explicitly saved | `Member EDIT08 saved` | PASS |
| Baseline verification | Independent Browse shows the six canonical lines | Six canonical lines shown | PASS |
| Edit Profile baseline | Current profile captured before mutation | `RECOVERY OFF WARN`, `AUTOSAVE ON`, `STATS ON`, other profile state captured | PASS |
| CANCEL rollback | Unsaved line-3 modification does not persist | Browse restored `LINE-03-CANCEL-TEST` | PASS |
| SAVE persistence | Explicitly saved line-4 modification survives leaving Edit | Browse showed `LINE-04-SAVED-CHANGE` | PASS |
| Restore baseline | Saved change can be reversed deliberately | `LINE-04-SAVE-TEST` restored and saved | PASS |
| Post-recovery validation | Independent Browse equals canonical baseline | Final Browse matches all six canonical lines | PASS |
| Final persistent state | No experimental mutation remains | Baseline restored | PASS |
| Publication review | No unnecessary sensitive host/network data intentionally included | Review approved; text pattern scan clean | PASS |

## Acceptance decision

**VALIDATED — M3 Resilient**

The M3 classification is supported by an executed rollback path and independent post-recovery validation, not only by a documented recovery intention.
