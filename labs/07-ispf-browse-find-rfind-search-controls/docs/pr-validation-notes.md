# Pull Request Validation Notes — Lab 07

## Objective

Add Lab 07 validating ISPF Browse FIND, RFIND and targeted search controls.

## Architecture V2

```text
Domain: Operations and Service Management
Capability: ISPF Browse targeted data search and read-only inspection
Lifecycle: Operate / Observe
Maturity: M1 — Foundational
Integration level: I0 — Standalone
Validation status: VALIDATED
```

## Validation performed

- basic FIND;
- RFIND;
- ALL with 21 observed matches;
- FIRST;
- LAST;
- reverse RFIND behavior after LAST;
- default case-insensitive text search;
- case-sensitive uppercase character-string search;
- deliberate lowercase case-sensitive not-found result;
- CHARS;
- WORD;
- PREFIX;
- exact-column search;
- column-range search;
- hexadecimal byte search;
- picture-string search;
- Browse termination to member list.

## Result

Lab validated successfully.

No persistent z/OS object was modified.

No batch RC applies.

## Negative test

`FIND C'member' FIRST` returned the expected not-found result while ordinary text-mode `FIND member FIRST` found uppercase `MEMBER`.

## Rollback

Not required.

All validation was read-only.

## Publication security

Reviewed and approved.

See `security-review.md`.

## Next capability

ISPF Edit fundamentals.
