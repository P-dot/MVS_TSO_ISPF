# Technical Notes — Lab 13

## EXCLUDE is a display-state operation

`X`, `X3`, and `XX/XX` were validated as selective visibility controls.

The lab demonstrates that excluded records become represented by `LINE(S) NOT DISPLAYED` special lines while the underlying member data remains intact.

## Partial redisplay

`F` and `L` were executed directly against an excluded-block special line.

Observed:

```text
X3
 -> 3 hidden

F
 -> first hidden record restored
 -> 2 hidden remain

L
 -> last hidden record restored
 -> 1 hidden remains
```

## SHOW and indentation

The hierarchical fixture:

```text
ROOT
  CHILD-A
    GRANDCHILD-A
  CHILD-B
    GRANDCHILD-B
```

was excluded as a five-record block.

`S2` redisplayed:

```text
ROOT
  CHILD-A
```

while three records remained hidden.

This is direct environment evidence of indentation-aware SHOW behavior.

## Edit labels

Three user-defined labels were created:

```text
.START
.MID
.END
```

`L .MID` positioned to the middle label.

Built-in positioning was then validated with:

```text
L .ZLAST
L .ZFIRST
```

`RESET LABEL` removed the custom labels without changing member data.

## TABS scope boundary

The Chapter 15 TABS line command was used to expose the `=TABS>` special line.

The lab intentionally does not alter advanced tab configuration. That material belongs to a later capability and should not be pulled forward merely because the TABS line command is introduced here.

## Why M2

The lab is operationally repeatable and well observed, but it does not demonstrate an exceptional failure/diagnosis/recovery lifecycle.

Architecture V2 maturity therefore remains:

```text
M2 — Operational
```

This is deliberate evidence-based classification, not a missing achievement.
