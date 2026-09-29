# Technical Notes — Lab 15

## Primary EXCLUDE versus line-command EXCLUDE

Earlier labs validated positional line commands such as `X`, `X3`, and `XX/XX`.

Lab 15 validates the primary command, where selection is driven by command scope and content.

`X ALL DROP` excluded the two records containing `DROP`.

## Label-range EXCLUDE

User labels `.XA` and `.XB` were attached to the start/end of the target range.

The source-style shorthand `EXCLUDE .XA .XB` was not accepted by the tested environment and produced:

```text
Put string in quotes
```

The environment accepted:

```text
EXCLUDE ALL .XA .XB
```

which excluded the entire four-record label range.

The repository documents the observed syntax rather than silently replacing it with a theoretical form.

## DELETE and rollback

`DEL ALL X` converted excluded display state into an actual working-data deletion.

Observed:

```text
2 lines deleted
```

The working set therefore dropped from 17 to 15 records.

The mutation was intentionally not saved.

`CANCEL` restored the canonical 17-record member.

## SORT and rollback

Sorting was scoped by both:

- columns 6–7;
- labels `.SA` through `.SB`.

The block changed from:

```text
03
01
04
02
```

to:

```text
01
02
03
04
```

`CANCEL` restored the original sequence.

## Recursive Edit

The parent `EDIT15` session invoked:

```text
EDIT EDIT15R
```

The child member became the active Edit session while the parent was suspended.

Cancelling the child returned directly to the parent `EDIT15` session.

## M3 rationale

This lab demonstrates:

- destructive working-state mutation;
- explicit rollback;
- post-rollback canonical state;
- resequencing rollback;
- nested Edit context return.

That is sufficient evidence for `M3 — Resilient`.
