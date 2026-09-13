# Lab 07 — ISPF Browse FIND, RFIND and Search Controls

## Architecture metadata

```yaml
lab:
  historical_id: "labs/07-ispf-browse-find-rfind-search-controls"
  title: "ISPF Browse FIND, RFIND and Search Controls"
  status: "VALIDATED"

architecture:
  domain: "Operations and Service Management"
  capability: "ISPF Browse targeted data search and read-only inspection"
  lifecycle:
    - Operate
    - Observe
  maturity: "M1 — Foundational"
  integration_level: "I0 — Standalone"

dependencies:
  - "D1: Lab 06 — Browse display controls and Recursive Browse"
  - "D4: active TSO/E and ISPF environment"

validation:
  status: "VALIDATED"
  persistent_change: "NONE"
  batch_rc: "NOT APPLICABLE"

next_capability:
  - "ISPF Edit fundamentals"
```

## Objective

Validate the principal search capabilities of ISPF Browse:

- basic `FIND`;
- repeat search with `RFIND`;
- total-count search with `ALL`;
- `FIRST` and `LAST` direction control;
- the implied RFIND direction after `LAST`;
- normal text-mode case-insensitive behavior;
- case-sensitive character strings;
- string-context controls such as `CHARS`, `WORD` and `PREFIX`;
- column-specific and column-range search;
- hexadecimal byte search;
- picture-string search;
- a controlled not-found result.

## Engineering context

Labs 05 and 06 established movement, representation and nested inspection inside Browse.

Lab 07 adds targeted search:

```text
Browse
  |
  +--> navigate
  +--> represent
  +--> search     <- Lab 07
```

This closes the read-only Browse capability block before Edit is introduced.

## Scope

Included:

- FIND;
- RFIND;
- FIRST;
- LAST;
- ALL;
- CHARS;
- WORD;
- PREFIX;
- case-insensitive text search;
- case-sensitive character strings;
- column constraints;
- hexadecimal strings;
- picture strings;
- controlled not-found validation.

Excluded:

- CHANGE;
- EXCLUDE;
- Edit;
- JCL syntax validation;
- REXX automation.

## Preconditions

- TSO/E and ISPF active.
- `IBMUSER.JCL.LAB(L10PREP)` available.
- Labs 05 and 06 understood.
- Browse session positioned at a known starting point where required.

## Components involved

- TSO/E
- ISPF 6.1
- ISPF Browse
- PDS `IBMUSER.JCL.LAB`
- member `L10PREP`

## Procedure and observed results

### 1. Basic FIND

Command:

```text
FIND MEMBER
```

Observed:

```text
CHARS 'MEMBER' found
```

Evidence:

- `01-find-member-command.png`
- `02-find-member-first-result.png`

### 2. RFIND

PF5 / RFIND was used to move to the next occurrence without re-entering the FIND command.

Evidence:

- `03-rfind-next-occurrence.png`

This validates that ISPF preserves the previous FIND criteria for repeated searching.

### 3. FIND ALL

Command:

```text
FIND MEMBER ALL
```

Observed total:

```text
21 CHARS 'MEMBER'
```

Evidence:

- `04-find-member-all-command.png`
- `05-find-member-all-count-21.png`

The `ALL` option therefore provided a total occurrence count in addition to locating the search string.

### 4. FIRST

Command:

```text
FIND MEMBER FIRST
```

The search started from the beginning of the member and located the first occurrence.

Evidence:

- `06-find-member-first-result.png`

### 5. LAST and reverse RFIND direction

Command:

```text
FIND MEMBER LAST
```

located the last occurrence.

Evidence:

- `07-find-member-last-command.png`
- `08-find-member-last-result.png`

PF5 / RFIND was then used.

The repeat search proceeded toward the previous occurrence, demonstrating the reverse direction implied by `LAST`.

Evidence:

- `09-rfind-prev-after-last.png`

### 6. Default text mode is case-insensitive

Command:

```text
FIND member FIRST
```

was entered in lowercase.

The member contains uppercase `MEMBER`, and ISPF located it.

Evidence:

- `10-find-lowercase-command.png`
- `11-text-mode-case-insensitive-result.png`

This validates the default text-search behavior:

```text
member -> MEMBER
```

### 7. Case-sensitive character string

Command:

```text
FIND C'MEMBER' FIRST
```

located the exact uppercase character string.

Evidence:

- `12-character-string-uppercase-result.png`

A controlled negative test was later executed using:

```text
FIND C'member' FIRST
```

Observed:

```text
No CHARS 'member' found
```

Evidence:

- `20-case-sensitive-lowercase-not-found.png`

This closes the distinction:

```text
FIND member
      -> case-insensitive text search

FIND C'member'
      -> exact-case character search
      -> not found

FIND C'MEMBER'
      -> exact-case character search
      -> found
```

### 8. CHARS context

Command:

```text
FIND MEMBER CHARS
```

located `MEMBER` using the default character-context model.

Evidence:

- `13-find-member-chars-result.png`

`CHARS` permits the requested sequence to exist inside a larger character group.

### 9. WORD context

Command:

```text
FIND MEMBER WORD
```

located an occurrence where `MEMBER` satisfied whole-word context.

Evidence:

- `14-find-member-word-result.png`

### 10. PREFIX context

Command:

```text
F MEM PREFIX
```

located a word beginning with `MEM`.

Evidence:

- `15-find-mem-prefix-result.png`

The lab therefore validates multiple string-context controls without adding redundant context variations solely for coverage.

### 11. Exact starting column

Command:

```text
FIND '//' 1
```

located the JCL introducer beginning in column 1.

Evidence:

- `16-find-double-slash-column-1-result.png`

This demonstrates exact start-column search.

### 12. Column range

Command:

```text
FIND DSN 1 30 FIRST
```

located `DSN` within the specified column range.

Evidence:

- `17-find-dsn-column-range-result.png`

This is operationally important for fixed-format and column-sensitive mainframe data.

### 13. Hexadecimal search

Command:

```text
FIND X'40'
```

located byte value hexadecimal `40`, the EBCDIC blank.

Evidence:

- `18-find-hex-40-result.png`

This differs from searching for the visible characters `40`.

```text
FIND '40'   -> characters 4 and 0
FIND X'40'  -> one byte, hexadecimal 40
```

### 14. Picture-string search

Command:

```text
FIND P'##'
```

searched for two consecutive numeric characters.

The observed matching value was:

```text
10
```

Evidence:

- `19-find-picture-two-digits-result.png`

The `#` symbols are pattern classes, not literal hash characters.

### 15. Terminate Browse

PF3 / END returned to the member list for:

```text
IBMUSER.JCL.LAB
```

Evidence:

- `21-browse-ended-member-list.png`

No data was modified.

## Verified operations

| Capability | Observed result |
|---|---|
| `FIND MEMBER` | `MEMBER` found |
| PF5 / RFIND | next occurrence found |
| `FIND MEMBER ALL` | 21 occurrences reported |
| `FIRST` | first occurrence selected |
| `LAST` | last occurrence selected |
| RFIND after LAST | search proceeded upward / previous |
| `FIND member` | uppercase `MEMBER` found |
| `FIND C'MEMBER'` | exact uppercase string found |
| `FIND C'member'` | controlled not-found result |
| `CHARS` | character-context match |
| `WORD` | whole-word match |
| `PREFIX` | prefix-context match |
| `FIND '//' 1` | exact column-1 match |
| `FIND DSN 1 30 FIRST` | match inside column range |
| `FIND X'40'` | hexadecimal byte search |
| `FIND P'##'` | two-digit picture-string match |
| PF3 / END | returned to member list |

## Result

**Validation status: VALIDATED**

```text
Execution result: successful Browse search sequence
Validation result: FIND/RFIND search controls validated
Operational result: targeted read-only search capability established
Negative-test result: case-sensitive lowercase string correctly not found
Security result: publication review approved
Recovery result: not required; no persistent change
```

### Architecture V2 result

```text
Lifecycle stage: Operate / Observe
Maturity level: M1 — Foundational
Integration level: I0 — Standalone
Validation status: VALIDATED
```

## Failure / exception analysis

Lab 07 includes a deliberate negative search:

```text
FIND C'member' FIRST
```

The target contains uppercase `MEMBER` but no matching lowercase character string at the tested positions.

Observed:

```text
No CHARS 'member' found
```

This is a successful negative test rather than a lab failure.

Other possible failures such as unavailable data sets or authorization failures are outside this capability scope.

## Recovery / rollback

No persistent z/OS object was modified.

```text
Rollback: NOT REQUIRED
```

PF3 / END returned Browse to the member-list context.

## Security and publication review

The evidence contains:

- `IBMUSER`;
- lab-owned data-set/member names;
- visible lab JCL source;
- search messages and highlights.

The selected evidence does not intentionally contain:

- passwords;
- ADCD credential tables;
- private IP addresses;
- MAC addresses;
- VTAM terminal identifiers;
- host network configuration;
- tokens;
- private keys.

See `docs/security-review.md`.

## Cross-repository relationships

### JCL_LABS

Relationship tag:

```text
REL-JCL
```

The source being searched is JCL, but the engineering objective is ISPF Browse search.

JCL syntax and JES2 execution remain owned by `JCL_LABS`.

Integration remains:

```text
I0 — Standalone
```

### Low-level data inspection

`X'40'` search builds on the byte-representation capability validated in Lab 06.

This provides a useful prerequisite for future EBCDIC/binary-data investigation without claiming COBOL or Assembler validation.

### REXX / automation

Relationship tag:

```text
REL-AUTOMATION
```

Manual search capability is established before any ISPF/REXX automation is attempted.

## Lessons learned

- FIND defaults to text-mode, case-insensitive matching.
- `C'...'` enables exact-case character matching.
- RFIND preserves prior FIND criteria.
- `LAST` changes the implied RFIND direction to previous/upward.
- `ALL` can provide an occurrence count.
- `CHARS`, `WORD` and `PREFIX` change string-context semantics.
- Column restrictions are significant for positional mainframe records.
- `X'..'` searches bytes rather than visible hexadecimal characters.
- `P'..'` searches character classes rather than literal symbols.
- A not-found result can be an intentional validation outcome.

## Next capability

The Browse capability block is now complete.

The next lab should begin:

```text
ISPF Edit fundamentals
```

The next capability should focus on the differences between Browse and Edit, safe modification workflow, save/cancel behavior and controlled editing without yet mixing in the full advanced Editor command set.

## References

See the repository-level `references/README.md`.
