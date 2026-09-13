# Lab 05 — ISPF Browse Navigation, Scrolling, LOCATE and Labels

## Architecture metadata

```yaml
lab:
  historical_id: "labs/05-ispf-browse-navigation-scrolling-locate-labels"
  title: "ISPF Browse Navigation, Scrolling, LOCATE and Labels"
  status: "VALIDATED"

architecture:
  domain: "Operations and Service Management"
  capability: "ISPF read-only data inspection and navigation"
  lifecycle:
    - Discover
    - Operate
  maturity: "M1 — Foundational"
  integration_level: "I0 — Standalone"

relationships:
  components:
    - TSO/E
    - ISPF
    - PDS
  repositories:
    - MVS_TSO_ISPF

dependencies:
  - "D1: Lab 04 — data set and member-list processing"
  - "D4: active TSO/E and ISPF environment"

validation:
  status: "VALIDATED"
  persistent_change: "NONE"
  batch_rc: "NOT APPLICABLE"

next_capability:
  - "Advanced ISPF Browse commands"
```

## Objective

Validate safe, read-only navigation inside an ISPF Browse session and demonstrate how Browse position is controlled using:

- `PAGE`;
- `HALF`;
- numeric scroll amounts;
- `MAX`;
- `LOCATE` by line number;
- Browse labels;
- `LOCATE` by label;
- `END` / PF3 termination.

The lab deliberately stops before the advanced Browse command set and before `FIND`.

## Engineering context

Lab 04 validated the path from DSLIST into a partitioned data set and its member list.

Lab 05 extends that capability one layer deeper:

```text
ISPF
  |
  v
DSLIST
  |
  v
PDS member list
  |
  v
BROWSE
  |
  +--> scrolling
  +--> direct positioning
  +--> session labels
  |
  v
read-only inspection
```

The member contains JCL, but JCL semantics are not part of this lab. `IBMUSER.JCL.LAB` is used only as a real PDS containing sufficient data to exercise Browse navigation.

## Scope

Included:

- Browse of an existing PDS member;
- vertical navigation;
- scroll-amount control;
- line-number positioning;
- temporary Browse labels;
- safe termination.

Excluded:

- JCL semantics;
- source modification;
- Edit;
- `COLUMNS`;
- `DISPLAY`;
- `HEX`;
- recursive Browse;
- `FIND` / `RFIND`;
- REXX or ISPF automation.

## Preconditions

- TSO/E session active.
- ISPF active.
- `IBMUSER.JCL.LAB` available.
- `L10PREP` present in the PDS.
- Lab 04 concepts understood: DSLIST, member list and member selection.

## Components involved

- TSO/E
- ISPF 6.1
- DSLIST
- ISPF Browse
- PDS `IBMUSER.JCL.LAB`
- member `L10PREP`

## Procedure and observed results

### 1. Enter DSLIST

From the ISPF Primary Option Menu:

```text
=3.4
```

The Data Set List Utility was used with:

```text
IBMUSER.JCL.LAB
```

The data set was selected using Browse.

Evidence:

- `01-dslist-select-jcl-lab.png`

### 2. Select `L10PREP`

The PDS member list was displayed and `L10PREP` was selected.

The member is long enough to make scroll behavior observable.

Evidence:

- `02-select-l10prep-member.png`

### 3. Establish the Browse baseline

ISPF opened:

```text
BROWSE  IBMUSER.JCL.LAB(L10PREP)
```

Initial position:

```text
Top of Data
```

The panel initially showed:

```text
Scroll ===> CSR
```

Evidence:

- `03-browse-initial-csr.png`

### 4. PAGE scrolling

The scroll amount was changed to:

```text
PAGE
```

PF8 / Down moved the Browse display by approximately a display page.

Evidence:

- `04-scroll-page-down.png`

### 5. HALF scrolling

The scroll amount was changed to:

```text
HALF
```

PF8 / Down moved a smaller portion of the member than PAGE.

Evidence:

- `05-scroll-half-down.png`

The same directional PF key therefore behaves differently according to the configured scroll amount.

### 6. Numeric scrolling

The scroll amount was changed to:

```text
10
```

PF8 / Down advanced the display by ten lines.

Evidence:

- `06-scroll-numeric-10.png`

This demonstrates that a numeric value can be retained as the active scroll amount.

### 7. MAX to the bottom

The scroll amount was set to:

```text
MAX
```

PF8 / Down moved directly to the lower boundary of the member:

```text
Bottom of Data
```

Evidence:

- `07-scroll-max-bottom.png`

An important observed detail is that after the MAX operation the scroll field returned to the prior numeric value (`0010`). The laboratory therefore records MAX as a temporary maximum-scroll request in this observed ISPF session rather than assuming persistent behavior.

### 8. MAX to the top

MAX was entered again and PF7 / Up was used.

The Browse display returned to:

```text
Top of Data
```

Evidence:

- `08-scroll-max-top.png`

### 9. LOCATE by line number

The primary command:

```text
L 40
```

was executed.

ISPF positioned line 40 at the top of the Browse data display.

Evidence:

- `09-locate-line-40.png`

This is distinct from normal scrolling:

```text
scrolling -> current position + direction + amount
LOCATE    -> explicit target position
```

### 10. Assign a Browse label

At the selected position, the command:

```text
.MARK
```

was issued.

ISPF responded:

```text
Label '.MARK' assigned
```

Evidence:

- `10-label-mark-assigned.png`

The label is Browse-session state. It does not modify the member.

### 11. Return to the saved position

After moving away from the labelled position, the command:

```text
L MARK
```

was issued.

ISPF responded:

```text
Label 'MARK' located
```

and returned to the saved Browse position.

Evidence:

- `11-label-mark-located.png`

The validated sequence is:

```text
L 40
  |
  v
.MARK
  |
  v
move away
  |
  v
L MARK
  |
  v
saved position restored
```

### 12. Terminate Browse

PF3 / END terminated the member Browse session and returned to the PDS member-list context.

Evidence:

- `12-browse-ended-member-list.png`

No save operation was required because the session was read-only.

## Expected result

The user can navigate a member without modification and can:

- control scroll granularity;
- move to top/bottom boundaries;
- jump directly to a line;
- create a temporary semantic position marker;
- return to the labelled position;
- terminate Browse safely.

## Evidence

Selected evidence is stored in:

```text
evidence/
```

Twelve screenshots were retained from the working document. Repetitive intermediate frames were deliberately excluded.

## Result

**Validation status: VALIDATED**

```text
Execution result: successful interactive Browse sequence
Validation result: expected navigation behavior observed
Operational result: safe read-only inspection validated
Security result: no credentials or private network details selected for publication
Recovery result: not required; no persistent z/OS change was made
Publication result: text scan clean
```

### Architecture V2 result

```text
Lifecycle stage: Discover / Operate
Maturity level: M1 — Foundational
Integration level: I0 — Standalone
Validation status: VALIDATED
```

The lab satisfies M1 because the procedure, inputs, expected behavior and evidence are repeatable and understood.

It is not classified M2 because no service administration, runtime failure handling or operational recovery capability is being claimed.

## Failure or exception analysis

No artificial failure was introduced.

This is appropriate for the M1 objective because the lab validates a read-only navigation capability.

Potential user-level exceptions for later study include:

- locating an invalid line number;
- locating an undefined label;
- attempting Browse against an unsupported data-set type;
- insufficient authority to the target data set.

Those cases were not validated here and are not claimed as completed functionality.

## Recovery / rollback

No persistent system or data-set change was performed.

Rollback:

```text
Not required
```

Leaving Browse with PF3 / END returned to the member list.

## Security and publication review

The selected evidence contains:

- `IBMUSER`;
- ISPF panel information;
- lab-owned data-set/member names;
- JCL source text used only as read-only navigation data.

The selected evidence does not contain:

- passwords;
- ADCD credential tables;
- private IP addresses;
- MAC addresses;
- VTAM terminal identifiers;
- host network adapter information;
- tokens or private keys.

See:

```text
docs/security-review.md
```

## Cross-repository relationships

### JCL_LABS

Relationship tag:

```text
REL-JCL
```

`IBMUSER.JCL.LAB(L10PREP)` is used as Browse input, but Lab 05 does not validate JCL syntax or JES2 execution.

Therefore the integration level remains:

```text
I0 — Standalone
```

### REXX

Relationship tag:

```text
REL-AUTOMATION
```

The manual Browse capability contributes to the longer-term operations-automation learning path:

```text
MVS_TSO_ISPF
      |
      v
manual operator capability
      |
      v
REXX / ISPF services
      |
      v
controlled automation
```

No REXX automation is performed in this lab.

## Lessons learned

- Browse provides safe read-only inspection before Edit is introduced.
- PF7/PF8 direction and `SCROLL` amount are separate concepts.
- `PAGE`, `HALF` and numeric values change navigation granularity.
- `MAX` provides rapid boundary navigation and behaved as a temporary maximum request in the observed session.
- `LOCATE` is independent of the current position.
- Browse labels provide human-readable temporary position references.
- A Browse label belongs to the active Browse session and does not alter the member.

## Next capability

Lab 06 should advance from navigation to the advanced Browse command set:

```text
COLUMNS
RESET
DISPLAY
HEX
recursive Browse
```

`FIND` / `RFIND` should remain a subsequent focused capability rather than being mixed into the same lab.

## References

See the repository-level `references/README.md`.
