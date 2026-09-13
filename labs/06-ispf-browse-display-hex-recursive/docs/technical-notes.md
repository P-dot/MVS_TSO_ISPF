# Technical Notes — Lab 06

## COLUMNS

`COLUMNS` adds a positional ruler above Browse data.

It is a display aid and does not become part of the member.

The lab confirmed that the ruler remains available while the underlying data is vertically scrolled.

## RESET

In Browse, `RESET` removes temporary display state such as the column ruler.

This differs from member-list RESET behavior validated in Lab 04.

The broader lesson is that ISPF primary commands are interpreted in panel/function context.

## DISPLAY CC / NOCC

`DISPLAY CC` controls visibility of carriage-control information when such data is meaningful.

The selected JCL member did not expose a visible CC distinction.

The lab therefore validates the command path but does not claim a visual transformation unsupported by the target data.

## HEX ON VERT

Vertical hexadecimal Browse represents each logical character line with:

```text
character row
high-order hexadecimal digit row
low-order hexadecimal digit row
```

The two hexadecimal rows can be combined by column to obtain the byte value of each character.

This is especially useful when visible characters alone do not explain the data.

## HEX ON DATA

`HEX ON DATA` changes to the alternative hexadecimal data layout.

The exact density and visual layout are panel/environment characteristics and are documented from observed ISPF 6.1 evidence.

## HEX OFF

`HEX OFF` restores conventional character Browse.

The lab deliberately turns HEX off before continuing so that display-state changes do not leak into later validation steps.

## Recursive Browse

`BROWSE CALLPRC2` was issued from `L10PREP`.

The parent session remained suspended below the nested session.

Conceptually:

```text
Browse stack

CALLPRC2   <- active
L10PREP    <- suspended
```

One END produced:

```text
L10PREP    <- active again
```

A second END returned to the PDS member list.

## Architecture V2 classification rationale

### Domain

**Operations and Service Management**

The objective is operator-side inspection and ISPF productivity.

### Lifecycle

**Operate / Observe**

The lab actively operates Browse controls and changes how the operator observes data.

### Maturity

**M1 — Foundational**

The procedure is safe, repeatable, bounded and evidenced.

No failure/recovery or automation maturity is claimed.

### Integration

**I0 — Standalone**

Although JCL source is viewed and HEX has future value to other domains, only ISPF Browse capability is validated here.
