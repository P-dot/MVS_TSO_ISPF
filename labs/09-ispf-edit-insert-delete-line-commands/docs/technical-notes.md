# Technical Notes — Lab 09

## Line-command semantics

`I`, `D`, `D3`, and `DD` are line commands entered in the line-command area.

A transient `Invalid command name` message was captured. The exact invalid input is not visible, so the repository records the symptom without inventing a root cause.

## INSERT

`I` opened one input record. `I3` opened three. The working count progressed 13 -> 14 -> 17.

`CANCEL` discarded the insert working state and Browse verified the 13-record baseline.

## DELETE

`D` removed one record. `D3` removed three records. The working count progressed 13 -> 12 -> 9.

## Pending block recovery

A single `DD` produced `Block command incomplete`. `RESET` cleared the pending block command while preserving all block records.

## Completed block delete

`DD` on the first and last block records removed the contiguous block. Six working records remained.

`CANCEL` discarded the destructive sequence and independent Browse verified the original 13 records.

## M3 rationale

The executed evidence includes rollback, abnormal-state recognition, recovery with `RESET`, destructive-change containment, and independent post-recovery validation. The promotion from planned M2 to M3 is therefore evidence-driven.
