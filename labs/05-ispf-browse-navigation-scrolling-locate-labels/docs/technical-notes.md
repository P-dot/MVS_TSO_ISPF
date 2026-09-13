# Technical Notes — Lab 05

## Browse versus Edit

This lab intentionally uses ISPF Browse as a read-only inspection capability.

The engineering objective is operator navigation, not content modification.

```text
Browse -> inspect and navigate
Edit   -> modify and manage changed content
```

Edit is a future capability and is not inferred from Browse behavior.

## Scroll direction versus scroll amount

Browse navigation separates two decisions:

```text
direction:
UP / DOWN / PF7 / PF8

amount:
PAGE / HALF / numeric / MAX / CSR
```

The same PF key can therefore produce a different displacement depending on the active scroll amount.

## PAGE

`PAGE` moves approximately one display page.

The exact visible overlap and number of data lines depend on terminal layout and panel geometry, so the lab records observed behavior rather than assuming an invariant line count.

## HALF

`HALF` moves approximately half the page amount.

It is useful when a full page jump loses too much context.

## Numeric scroll amount

A numeric scroll amount such as:

```text
10
```

requests movement by that number of data lines when combined with a direction.

In the observed session the numeric amount was retained in the scroll field.

## MAX observation

The lab used:

```text
MAX + PF8
MAX + PF7
```

to reach bottom and top boundaries.

The evidence also showed an important session behavior:

```text
previous scroll amount = 0010
MAX operation executed
scroll field returns to 0010
```

The documentation therefore records MAX as a temporary maximum-scroll request for this tested environment.

## LOCATE by line number

`L 40` does not mean “scroll 40 lines.”

It means:

```text
position line 40 at the top of the Browse display
```

The target is explicit and does not depend on the current location.

## Browse labels

The command:

```text
.MARK
```

assigned a temporary label to the line currently positioned at the top of Browse.

The system confirmed:

```text
Label '.MARK' assigned
```

The label exists only as Browse-session navigation state.

It does not become part of the PDS member.

## LOCATE by label

After moving away, the command:

```text
L MARK
```

returned to the labelled position.

The system confirmed:

```text
Label 'MARK' located
```

This demonstrates a useful operator pattern:

```text
locate position
      |
      v
assign semantic label
      |
      v
inspect elsewhere
      |
      v
return by label
```

## Termination

PF3 / END terminated the active member Browse and returned to the PDS member-list context.

No SAVE semantics apply because no data was edited.

## Architecture V2 classification rationale

### Domain

**Operations and Service Management**

The objective is efficient operator interaction with ISPF, not the semantics of the content being viewed.

### Maturity

**M1 — Foundational**

The capability is:

- understood;
- repeatable;
- read-only;
- evidenced;
- bounded in scope.

It does not yet address operational failures, recovery or automated evidence collection.

### Integration

**I0 — Standalone**

Although the Browse target is a JCL member, `JCL_LABS` is not being executed or validated.

Using an artifact owned by another domain does not by itself create a cross-repository integration proof.
