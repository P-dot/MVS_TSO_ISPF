# Pull Request Validation Notes — Lab 09

## Objective

Add Lab 09 validating ISPF Edit INSERT and DELETE line-command semantics using deterministic record-count transitions and controlled rollback.

## Architecture V2

Domain: Operations and Service Management

Capability: Controlled ISPF Edit record insertion and deletion

Lifecycle: Baseline / Configure / Operate / Observe / Recover

Maturity: M3 — Resilient

Integration: I0 — Standalone

## Validation

- baseline 13 records;
- `I`: 13 -> 14;
- `I3`: 14 -> 17;
- CANCEL + independent Browse -> 13;
- `D`: 13 -> 12;
- `D3`: 12 -> 9;
- pending `DD` -> `Block command incomplete`;
- `RESET` cleared pending DD without deleting data;
- complete `DD` / `DD`: 9 -> 6;
- CANCEL + independent Browse -> 13.

A transient `Invalid command name` was observed; exact cause is not claimed because the evidence does not expose the input.

Final state: BASELINE RESTORED.

Next: Repeat, Copy, Move, Before and After.
