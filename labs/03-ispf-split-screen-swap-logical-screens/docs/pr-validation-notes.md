# Pull Request Validation Notes — Lab 03

## Objective

Add Lab 03 validating ISPF logical-screen operation with SPLIT, SWAP, SWAP LIST and END.

## Scope

MVS_TSO_ISPF interactive foundation only.

## Systems/components affected

- TSO/E session
- ISPF 6.1
- 3270 interactive session

## Validation performed

- additional logical-screen context created;
- Edit and Utilities kept in separate logical screens;
- F9/SWAP preserved independent panel state;
- SWAP LIST showed two active logical sessions;
- one logical screen was ended;
- final SWAP LIST showed one remaining logical session.

## Expected result

Successful logical-screen lifecycle validation. No batch RC applies.

## Negative test

Not applicable to this navigation-focused lab.

## Rollback

The runtime work is session-only. Repository rollback is deletion/reversion of the Lab 03 branch or commit before merge.

## Publication-security review

Completed. See `security-review.md`.

## Related repositories

- MVS_TSO_ISPF provides the interactive foundation.
- Rexx is the downstream automation consumer.
- JCL_LABS is a downstream interactive workflow consumer.
