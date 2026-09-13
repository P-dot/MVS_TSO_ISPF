# Lab 06 — ISPF Browse Display Controls, HEX and Recursive Browse

## Architecture metadata

```yaml
lab:
  historical_id: "labs/06-ispf-browse-display-hex-recursive"
  title: "ISPF Browse Display Controls, HEX and Recursive Browse"
  status: "VALIDATED"

architecture:
  domain: "Operations and Service Management"
  capability: "ISPF Browse data representation and nested read-only inspection"
  lifecycle:
    - Operate
    - Observe
  maturity: "M1 — Foundational"
  integration_level: "I0 — Standalone"

dependencies:
  - "D1: Lab 05 — Browse navigation and positioning"
  - "D4: active TSO/E and ISPF environment"

validation:
  status: "VALIDATED"
  persistent_change: "NONE"
  batch_rc: "NOT APPLICABLE"

next_capability:
  - "ISPF Browse FIND and RFIND"
```

## Objective

Validate advanced read-only ISPF Browse controls for:

- column-position visualization with `COLUMNS`;
- display-state cleanup with `RESET`;
- carriage-control display modes with `DISPLAY CC` and `DISPLAY NOCC`;
- EBCDIC byte representation using hexadecimal Browse modes;
- nested read-only inspection using Recursive Browse;
- restoration of the parent Browse session after ending the nested session.

## Engineering context

Lab 05 validated movement inside a Browse session.

Lab 06 advances from **where the operator is positioned** to **how the data is represented and how Browse contexts can be nested**.

```text
Browse navigation
      |
      v
Browse representation
      |
      +--> column ruler
      +--> display controls
      +--> hexadecimal representation
      +--> nested Browse
```

## Scope

Included:

- `COLUMNS`;
- vertical scrolling while COLUMNS remains active;
- `RESET`;
- `DISPLAY CC`;
- `DISPLAY NOCC`;
- `HEX ON VERT`;
- `HEX ON DATA`;
- `HEX OFF`;
- Recursive Browse of another member in the same PDS;
- END from nested Browse;
- END from parent Browse.

Excluded:

- `FIND`;
- `RFIND`;
- Edit;
- JCL semantics;
- source modification;
- REXX automation.

## Preconditions

- TSO/E and ISPF active.
- `IBMUSER.JCL.LAB` available.
- `L10PREP` available.
- `CALLPRC2` available.
- Lab 05 Browse concepts understood.

## Components involved

- TSO/E
- ISPF 6.1
- ISPF Browse
- PDS `IBMUSER.JCL.LAB`
- members `L10PREP` and `CALLPRC2`

## Procedure and observed results

### 1. COLUMNS

From Browse of:

```text
IBMUSER.JCL.LAB(L10PREP)
```

the command:

```text
COLUMNS
```

was executed.

ISPF added a column ruler above the displayed data.

Evidence:

- `01-columns-command.png`
- `02-columns-ruler.png`

### 2. COLUMNS persists during vertical scroll

PF8 / Down was used while the ruler remained active.

The data moved while the column ruler remained available as a positional reference.

Evidence:

- `03-columns-persist-after-scroll.png`

### 3. RESET

The command:

```text
RESET
```

was executed.

The Browse display returned to the normal data-only representation and the COLUMNS ruler was removed.

Evidence:

- `04-reset-command.png`
- `05-reset-columns-removed.png`

This is context-specific behavior. In Lab 04, RESET cleared pending member-list commands. In Browse, it resets Browse display state.

### 4. DISPLAY CC

The command:

```text
DISPLAY CC
```

was accepted.

The selected JCL member did not provide an observable carriage-control difference.

Evidence:

- `06-display-cc-command.png`

Correct interpretation:

```text
command accepted
      |
      v
selected source does not expose
an observable CC presentation difference
```

No visual effect is claimed beyond what the evidence proves.

### 5. DISPLAY NOCC

The command:

```text
DISPLAY NOCC
```

was then used to restore the default no-carriage-control presentation.

Evidence:

- `07-display-nocc-command.png`

Again, the selected JCL data does not provide a strong visible CC contrast; the lab records command behavior without inventing data that is not present.

### 6. HEX ON VERT

The command:

```text
HEX ON VERT
```

enabled vertical hexadecimal representation.

Each displayed character row was accompanied by high-order and low-order hexadecimal digit rows.

Evidence:

- `08-hex-on-vert.png`

This creates a direct relationship between visible EBCDIC characters and their underlying byte values.

### 7. HEX ON DATA

The hexadecimal mode was changed to:

```text
HEX ON DATA
```

The data was shown using the alternative hexadecimal Browse layout.

Evidence:

- `09-hex-on-data.png`

### 8. HEX OFF

The command:

```text
HEX OFF
```

returned Browse to the conventional character representation.

Evidence:

- `10-hex-off-normal-browse.png`

The validated representation cycle is:

```text
normal Browse
      |
      v
HEX ON VERT
      |
      v
vertical byte representation
      |
      v
HEX ON DATA
      |
      v
alternative hex representation
      |
      v
HEX OFF
      |
      v
normal Browse
```

### 9. Recursive Browse

While still browsing:

```text
IBMUSER.JCL.LAB(L10PREP)
```

the command:

```text
BROWSE CALLPRC2
```

was executed.

Evidence:

- `11-recursive-browse-command.png`

A second Browse session opened:

```text
IBMUSER.JCL.LAB(CALLPRC2)
```

Evidence:

- `12-recursive-browse-callprc2.png`

The original `L10PREP` Browse was suspended rather than terminated.

### 10. Return to parent Browse

PF3 / END was used once.

ISPF returned from:

```text
CALLPRC2
```

to:

```text
L10PREP
```

Evidence:

- `13-return-to-parent-browse.png`

This validates the nested Browse stack:

```text
Browse #1: L10PREP
      |
      v
Browse #2: CALLPRC2
      |
      | END
      v
Browse #1: L10PREP restored
```

### 11. End parent Browse

PF3 / END was used again.

ISPF returned to the PDS member list:

```text
BROWSE  IBMUSER.JCL.LAB
```

Evidence:

- `14-return-to-member-list.png`

This closes the full recursive lifecycle.

## Expected result

The user can:

- add and remove a Browse column ruler;
- change display behavior without modifying the member;
- inspect byte-level EBCDIC representation;
- switch among hexadecimal layouts;
- return to normal character display;
- open a nested Browse session;
- terminate the nested session and restore the parent Browse;
- terminate the parent Browse and return to the member list.

## Evidence

Fourteen screenshots are retained in `evidence/`.

The source working document contained additional intermediate frames; duplicates were excluded from the repository package.

## Result

**Validation status: VALIDATED**

```text
Execution result: successful interactive Browse sequence
Validation result: display controls, HEX modes and Recursive Browse validated
Operational result: advanced read-only inspection capability established
Security result: publication review approved
Recovery result: not required; no persistent change
Publication result: text IP/MAC scan clean
```

### Architecture V2 result

```text
Lifecycle stage: Operate / Observe
Maturity level: M1 — Foundational
Integration level: I0 — Standalone
Validation status: VALIDATED
```

## Failure or exception analysis

No controlled failure was required for the M1 objective.

One important content-dependent condition was observed:

```text
DISPLAY CC
```

did not create a meaningful visual difference in the selected JCL member.

This is recorded as a data-characteristic limitation, not a command failure.

Unvalidated exceptions include:

- invalid Recursive Browse member;
- unavailable member;
- insufficient read authority;
- unsupported data-set characteristics;
- non-displayable data requiring different representation.

No claims are made for those cases.

## Recovery / rollback

No persistent z/OS object was modified.

```text
Rollback: NOT REQUIRED
```

`HEX OFF`, `RESET` and `END` restored the expected interactive display/context state.

## Security and publication review

The selected evidence contains:

- `IBMUSER`;
- lab data-set/member names;
- visible lab-owned JCL;
- hexadecimal representation of the same lab data.

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

JCL members provide Browse input only.

JCL semantics and JES2 execution remain owned by `JCL_LABS`.

Integration remains:

```text
I0 — Standalone
```

because no JCL capability is being validated across repositories.

### Low-level / application consumers

HEX Browse is a useful prerequisite for understanding representations encountered later in:

- COBOL data;
- Assembler;
- EBCDIC;
- packed/binary data;
- diagnostic work.

Those capabilities are not claimed as validated by this lab.

### REXX / automation

Relationship tag:

```text
REL-AUTOMATION
```

The lab strengthens the manual capability baseline that later ISPF/REXX automation may consume.

No automation is performed here.

## Lessons learned

- `COLUMNS` provides a stable positional ruler while data scrolls.
- `RESET` is context-dependent in ISPF.
- `DISPLAY CC` is data-dependent; command acceptance does not guarantee a visually meaningful difference.
- hexadecimal Browse exposes the byte representation beneath characters.
- `HEX ON VERT` and `HEX ON DATA` are different presentation modes.
- `HEX OFF` should be used deliberately before unrelated work.
- Recursive Browse creates a nested Browse context instead of replacing the parent.
- END unwinds the Browse stack one level at a time.

## Next capability

Lab 07 should focus exclusively on:

```text
FIND
RFIND
direction
case sensitivity
search context
column boundaries
hexadecimal strings
picture strings
```

That keeps the chapter/capability boundary clean.

## References

See the repository-level `references/README.md`.
