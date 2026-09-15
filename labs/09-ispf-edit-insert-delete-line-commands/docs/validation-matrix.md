# Validation Matrix — Lab 09

| Test | Expected working state | Observed | Status |
|---|---|---|---|
| Baseline | 13 records | 13-record fixture saved | PASS |
| `I` | 14 | one insert record added | PASS |
| `I3` | 17 | three additional insert records added | PASS |
| CANCEL after inserts | persistent 13 | independent Browse shows canonical baseline | PASS |
| `D` | 12 | `DEL-SINGLE` removed | PASS |
| `D3` | 9 | `DEL-MULTI-A/B/C` removed | PASS |
| single `DD` | pending block | `Block command incomplete` | PASS |
| `RESET` | pending DD cleared, still 9 | data preserved | PASS |
| `DD` / `DD` | 6 | A/B/C block removed | PASS |
| final CANCEL | persistent 13 | independent Browse shows canonical baseline | PASS |

## Maturity decision

**M3 — Resilient**

The lab was planned as M2, but the evidence supports M3 because rollback, incomplete-block recovery, and independent post-recovery validation were all executed.
