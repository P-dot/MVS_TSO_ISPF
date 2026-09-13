# Technical Notes — Lab 07

## FIND baseline

The minimum FIND command consists of the search string.

The default search context is CHARS and the default direction is NEXT.

## RFIND

RFIND repeats the previous FIND criteria.

The lab used PF5, which is mapped to Rfind in the observed ISPF environment.

## ALL

`FIND MEMBER ALL` reported 21 occurrences.

The count is a useful distinction from an ordinary first-match search.

## FIRST and LAST

`FIRST` starts from the top regardless of current position.

`LAST` starts from the bottom and changes the implied repeat-search direction to PREV.

The lab observed this behavior with RFIND after LAST.

## Case handling

Default text search is case-insensitive:

```text
FIND member
```

found uppercase:

```text
MEMBER
```

Character-string notation is case-sensitive:

```text
FIND C'MEMBER'
```

found the uppercase form, while:

```text
FIND C'member'
```

returned a not-found message.

## Context controls

The lab validated:

```text
CHARS
WORD
PREFIX
```

These control where the requested string is valid relative to word boundaries.

## Columns

A single column specifies the exact starting column.

A start/end pair restricts the full matching string to that range.

This capability is especially relevant for positional mainframe records.

## Hexadecimal strings

`X'40'` represents one hexadecimal byte, not the characters `4` and `0`.

The lab used the EBCDIC blank value to validate byte-oriented search.

## Picture strings

`P'##'` uses `#` as the numeric-character class.

The observed match included the numeric pair `10`.

## Negative test

The deliberate case-sensitive lowercase search provided a useful M1 negative validation:

```text
input understood
      |
      v
no exact matching data
      |
      v
not-found message
```

No recovery action was required because no state was modified.

## Architecture V2 classification rationale

### Domain

**Operations and Service Management**

The capability improves operator-side data inspection and navigation.

### Lifecycle

**Operate / Observe**

The user actively operates ISPF search controls to observe targeted data.

### Maturity

**M1 — Foundational**

The capability is repeatable, safe, bounded and evidenced, including one controlled negative result.

### Integration

**I0 — Standalone**

JCL is only the test content; no JCL runtime or cross-repository behavior is validated.
