# Lab 08 — ISPF Edit Fundamentals: Controlled Modify, CANCEL, SAVE and Restore

## Architecture metadata

```yaml
lab:
  historical_id: "labs/08-ispf-edit-controlled-save-cancel-restore"
  title: "ISPF Edit Fundamentals: Controlled Modify, CANCEL, SAVE and Restore"
  status: "VALIDATED"

architecture:
  domain: "Operations and Service Management"
  capability: "Controlled ISPF Edit transaction lifecycle and safe data modification"
  lifecycle:
    - Baseline
    - Configure
    - Operate
    - Observe
    - Recover
  maturity: "M3 — Resilient"
  integration_level: "I0 — Standalone"

dependencies:
  - "D1: Lab 07 — Browse FIND/RFIND and targeted search"
  - "D4: active TSO/E and ISPF environment"
  - "D4: repository-owned PDS IBMUSER.ISPF.LAB"

validation:
  status: "VALIDATED"
  rollback: "VALIDATED"
  persistence: "VALIDATED"
  recovery: "VALIDATED"
  post_recovery_validation: "PASS"
  persistent_final_state: "BASELINE RESTORED"
  batch_rc: "NOT APPLICABLE"

next_capability:
  - "ISPF Edit line-command fundamentals: insert and delete"
```

## Objective

Introduce ISPF Edit as a controlled state-changing capability rather than as a simple text-entry exercise.

The lab validates:

- creation of a repository-owned Edit fixture;
- deterministic baseline creation;
- explicit initial `SAVE`;
- independent Browse validation;
- Edit Profile baseline capture;
- controlled unsaved modification;
- explicit `CANCEL` rollback;
- post-rollback verification;
- controlled persisted modification;
- explicit `SAVE`;
- post-save persistence verification;
- controlled restoration to the canonical baseline;
- independent post-recovery verification.

## Engineering context

Labs 05–07 were read-only.

Lab 08 crosses an important boundary:

```text
inspection
    |
    v
state-changing operation
```

For that reason the lab does not edit `IBMUSER.JCL.LAB`.

Instead it creates a repository-owned test boundary:

```text
IBMUSER.ISPF.LAB(EDIT08)
```

with a canonical GitHub-side baseline:

```text
fixtures/edit/EDIT08-baseline.txt
```

## Scope

Included:

- PDS fixture allocation;
- member creation;
- direct text overtype;
- `PROFILE 9`;
- `SAVE`;
- `CANCEL`;
- persistence validation;
- rollback validation;
- controlled restoration;
- independent final validation.

Excluded:

- insert/delete line commands;
- copy/move/repeat commands;
- `UNDO`;
- enabling `RECOVERY ON`;
- profile modification;
- JCL semantics;
- SUBMIT/JES2 integration;
- Edit macros.

## Repository-owned fixture

### PDS

```text
IBMUSER.ISPF.LAB
```

Observed allocation inputs:

```text
Organization:      PDS
Record format:     FB
Record length:     80
Block size:        0
Space unit:        TRACK
Primary quantity:  1
Secondary quantity:1
Directory blocks:  10
```

### Member

```text
EDIT08
```

### Canonical baseline

```text
ISPF-LAB08-BASELINE
LINE-02-UNCHANGED
LINE-03-CANCEL-TEST
LINE-04-SAVE-TEST
LINE-05-UNCHANGED
ISPF-LAB08-END
```

## Phase 1 — Initial member creation

The six-line baseline was entered in a new Edit session and explicitly saved.

Observed:

```text
Member EDIT08 saved
```

An independent Browse session showed the exact baseline.

Evidence:

- `01-allocate-ispf-lab-pds.png`
- `02-edit08-new-member-baseline-before-save.png`
- `03-edit08-initial-save-confirmation.png`
- `04-edit08-baseline-browse.png`

## Phase 2 — Edit Profile baseline

`PROFILE 9` was executed before the first mutation.

Observed profile state included:

```text
LAB (FIXED - 80)
RECOVERY OFF WARN
NUMBER OFF
CAPS ON
HEX OFF
NULLS ON STD
TABS OFF
AUTOSAVE ON
AUTONUM OFF
AUTOLIST OFF
STATS ON
PROFILE UNLOCK
IMACRO NONE
PACK OFF
NOTE ON
HILITE DEFAULT CURSOR FIND
```

The panel also warned that UNDO was unavailable until the profile is changed to `RECOVERY ON`.

The lab records this state without changing it.

Evidence:

- `05-profile-9-command.png`
- `06-edit-profile-baseline.png`

## Phase 3 — CANCEL rollback transaction

Original persistent record:

```text
LINE-03-CANCEL-TEST
```

Working-state modification:

```text
LINE-03-CANCELLED-CHANGE
```

The session was terminated using:

```text
CANCEL
```

Independent Browse then showed:

```text
LINE-03-CANCEL-TEST
```

Result:

```text
ROLLBACK PASS
```

Evidence:

- `07-unsaved-cancel-change.png`
- `08-cancel-command.png`
- `09-cancel-rollback-browse-validated.png`

## Phase 4 — SAVE persistence transaction

Original record:

```text
LINE-04-SAVE-TEST
```

Working-state modification:

```text
LINE-04-SAVED-CHANGE
```

Command:

```text
SAVE
```

Observed:

```text
Member EDIT08 saved
```

The session was then left with `CANCEL`, and an independent Browse showed:

```text
LINE-04-SAVED-CHANGE
```

The saved change therefore survived the Edit session.

Result:

```text
PERSISTENCE PASS
```

Evidence:

- `10-unsaved-save-change.png`
- `11-explicit-save-command.png`
- `12-save-confirmation-version-01-01.png`
- `13-cancel-after-save.png`
- `14-save-persistence-browse-validated.png`

## Phase 5 — Controlled restoration

The persisted experimental value:

```text
LINE-04-SAVED-CHANGE
```

was restored to:

```text
LINE-04-SAVE-TEST
```

and explicitly saved.

Observed:

```text
Member EDIT08 saved
```

The session was then exited using `CANCEL`.

Evidence:

- `15-baseline-restoration-save-command.png`
- `16-baseline-restoration-save-confirmation.png`
- `17-restored-edit-state.png`
- `18-cancel-after-restoration-save.png`

## Phase 6 — Independent post-recovery validation

A final Browse session showed exactly:

```text
ISPF-LAB08-BASELINE
LINE-02-UNCHANGED
LINE-03-CANCEL-TEST
LINE-04-SAVE-TEST
LINE-05-UNCHANGED
ISPF-LAB08-END
```

Evidence:

- `19-final-baseline-browse-post-recovery.png`

Result:

```text
POST-RECOVERY VALIDATION PASS
FINAL PERSISTENT STATE = BASELINE RESTORED
```

## State model

```text
known baseline
      |
      v
Edit working state
      |
      +---- CANCEL ----> baseline preserved
      |
      +---- SAVE ------> changed state persisted
                              |
                              v
                       controlled restore
                              |
                             SAVE
                              |
                              v
                       baseline restored
                              |
                              v
                       independent Browse
                              |
                              v
                             PASS
```

See `docs/state-transition-model.md`.

## Validation summary

| Capability | Result |
|---|---|
| Repository-owned Edit fixture | PASS |
| Initial baseline persistence | PASS |
| Profile baseline observation | PASS |
| Explicit CANCEL rollback | PASS |
| Independent rollback validation | PASS |
| Explicit SAVE persistence | PASS |
| Independent persistence validation | PASS |
| Controlled baseline restoration | PASS |
| Independent post-recovery validation | PASS |
| Final persistent state | BASELINE RESTORED |

See `docs/validation-matrix.md`.

## Operational interpretation

The key lesson is not simply that ISPF can edit text.

The lab demonstrates three distinct states:

```text
persistent member state
working Edit state
restored final state
```

and proves which command transitions between them.

Because `AUTOSAVE ON` was observed, the lab deliberately uses explicit `SAVE` and `CANCEL` instead of relying on PF3/END semantics.

## Failure / exception analysis

The rollback path is deliberately exercised rather than left hypothetical.

The lab also exposes an environmental limitation:

```text
RECOVERY OFF WARN
```

with a warning that UNDO is unavailable.

This does not fail Lab 08 because the capability being validated is explicit `SAVE`/`CANCEL` control, not Edit Recovery or UNDO.

A future dedicated recovery/profile lab should evaluate `RECOVERY ON`, UNDO behavior, recovery data and safe profile management.

## Recovery / rollback

Two recovery behaviors are proven:

1. pre-save rollback using `CANCEL`;
2. post-save controlled restoration followed by independent Browse verification.

The final persistent object equals the canonical fixture.

## Security and publication review

Evidence is synthetic and repository-owned.

The screenshots intentionally contain no passwords, private keys, tokens, private IP addresses, MAC addresses or host-side networking information.

See `docs/security-review.md`.

## Cross-repository relationships

### JCL_LABS

Labs 04–07 used JCL members only as read-only inspection data.

Lab 08 deliberately stops doing that for state-changing tests.

Future:

```text
ISPF Edit -> JCL -> SUBMIT -> JES2 -> SDSF
```

should be treated as an explicit integration scenario rather than hidden inside a basic Edit lab.

### REXX / automation

Manual state-control semantics established here become prerequisites for safe future ISPF/REXX automation.

No automation is claimed by this lab.

## Architecture V2 result

```text
Lifecycle stage:
Baseline / Configure / Operate / Observe / Recover

Maturity level:
M3 — Resilient

Integration level:
I0 — Standalone

Validation status:
VALIDATED
```

The M3 classification is evidence-based: rollback, persistence, restoration and post-recovery validation were all executed.

## Lessons learned

- Read-only Browse and state-changing Edit require different lab-safety boundaries.
- Repository-owned fixtures prevent accidental mutation of another domain's artifacts.
- `CANCEL` can be proven through independent post-rollback Browse.
- `SAVE` must be proven through a new session, not only through an on-screen message.
- A persisted experiment should end with controlled restoration when a canonical baseline is required.
- `PROFILE 9` should be observed before relying on assumptions about `AUTOSAVE`, `RECOVERY`, `CAPS`, `NUMBER` or `STATS`.
- `RECOVERY OFF WARN` means this lab must not claim UNDO/Recovery capability.
- Final state validation is part of the recovery procedure, not an optional screenshot.

## Next capability

**Lab 09 — ISPF Edit Line Commands: Controlled Insert and Delete**

Planned capability boundary:

```text
baseline
   |
   v
insert records
   |
   v
validate record count/content
   |
   v
delete records
   |
   v
restore canonical state
```

Copy/move/repeat remain later capabilities.

## References

See the repository-level `references/README.md`.
