# Lab 01 — TSO/E Logon, Native READY Mode and ISPF Environment

## Objective

Demonstrate, with evidence from a running z/OS 1.11 ADCD system, the relationship between the 3270 session, TSO/E, the TSO logon procedure, ISPF, the ISPF Command Shell, native TSO `READY` mode, and `LOGOFF`.

The key point is to prove experimentally that **ISPF runs within the TSO/E interactive session** and that terminating ISPF does not necessarily terminate TSO/E.

## Scope

This lab covers:

- entering the TSO logon flow from the ADCD session manager;
- observing the TSO/E logon panel;
- starting ISPF;
- identifying the ISPF Primary Option Menu and session information;
- running the TSO `PROFILE` command from ISPF option 6;
- terminating ISPF with `=X`;
- processing the ISPF log data set disposition panel;
- reaching the native TSO `READY` prompt;
- running `PROFILE` again from native TSO;
- terminating the TSO/E session with `LOGOFF`.

No batch job is submitted in this lab, so a JES step return code such as `RC=0000` is **not applicable**.

## Conceptual model

```text
3270 / TN3270
      |
      v
    z/OS
      |
      v
    TSO/E
      |
      +---- native TSO command environment ---- READY
      |
      +---- ISPF
             |
             +---- Primary Option Menu
             |
             +---- Option 6: ISPF Command Shell
                        |
                        +---- TSO commands
```

TSO/E establishes the interactive z/OS session and provides the native command environment. ISPF is a menu- and panel-driven interface used from that TSO/E environment.

## Executed flow

### 1. Enter TSO

From the ADCD session manager:

```text
L TSO
```

The system requested the TSO user ID and then displayed the TSO/E LOGON panel.

Observed values included:

```text
Userid    ===> IBMUSER
Procedure ===> DBSPROC9
Command   ===> ispf
```

The password value is not recorded in the published evidence.

### 2. ISPF startup

After successful TSO/E logon, ISPF started and the Primary Option Menu was displayed.

Observed ISPF/session information included:

```text
User ID . : IBMUSER
Terminal. : 3278
Screen. . : 1
Language. : ENGLISH
Appl ID . : ISR
TSO logon : DBSPROC
TSO prefix: IBMUSER
System ID : ADCD
Release . : ISPF 6.1
```

### Environment observation: DBSPROC9 vs DBSPROC

The TSO/E LOGON panel displayed `DBSPROC9`, while the ISPF Primary Option Menu displayed `DBSPROC` in the `TSO logon` field.

This lab records that difference exactly as observed and does **not** infer the cause. It can be investigated in a later lab focused on logon procedures and allocations.

### 3. Execute a native TSO command from ISPF

From the Primary Option Menu, option `6` opened the **ISPF Command Shell**.

The command executed was:

```text
PROFILE
```

The output included:

```text
PREFIX(IBMUSER)
PLANGUAGE(ENU)
SLANGUAGE(ENU)
VARSTORAGE(LOW)
```

The important result for this lab is:

```text
PREFIX(IBMUSER)
```

This matches the `TSO prefix: IBMUSER` value displayed by ISPF.

### 4. Terminate ISPF

From the ISPF Primary Option Menu:

```text
=X
```

ISPF displayed the **Specify Disposition of Log Data Set** panel. The session kept the log data set and reported:

```text
IBMUSER.SPFLOG1.LIST has been kept.
```

After ISPF termination, the system displayed:

```text
READY
```

This is the native TSO/E command prompt, not an ISPF panel.

### 5. Confirm the same TSO profile in native READY mode

From `READY`:

```text
PROFILE
```

The result again included:

```text
PREFIX(IBMUSER)
```

This demonstrates that the command executed from ISPF option 6 and the command executed after ISPF termination used the same TSO/E user context.

### 6. End the TSO/E session

From `READY`:

```text
LOGOFF
```

The session returned to the ADCD/session-manager entry screen. This marks the end of the TSO/E session.

## Result

**Lab 01 completed successfully.**

The observed flow was:

```text
ADCD / session manager
        |
        v
      L TSO
        |
        v
   TSO/E LOGON
        |
        +-- logon procedure observed
        +-- command ISPF
        |
        v
       ISPF
        |
        +-- Primary Option Menu
        |
        +-- Option 6
        |      |
        |      +-- PROFILE -> PREFIX(IBMUSER)
        |
       =X
        |
        v
  ISPF termination
        |
        v
      READY
        |
        +-- PROFILE -> PREFIX(IBMUSER)
        |
      LOGOFF
        |
        v
ADCD / session manager
```

The lab therefore demonstrates the layered relationship:

```text
z/OS -> TSO/E -> ISPF
```

and shows that leaving ISPF can expose native TSO `READY` mode while the TSO/E session remains active.

## Evidence

| # | Evidence | Demonstrates |
|---|---|---|
| 01 | `01-adcd-tso-entry-redacted.png` | ADCD entry screen and `L TSO` path; terminal/network identifier redacted |
| 02 | `02-tso-userid-prompt.png` | TSO user ID prompt |
| 03 | `03-tso-e-logon-panel.png` | TSO/E LOGON panel, procedure and ISPF command |
| 04 | `04-ispf-primary-option-menu.png` | ISPF Primary Option Menu and session information |
| 05 | `05-ispf-command-shell.png` | ISPF option 6 / Command Shell |
| 06 | `06-profile-command-inside-ispf.png` | `PROFILE` entered from ISPF |
| 07 | `07-profile-result-inside-ispf.png` | TSO profile result inside ISPF, including `PREFIX(IBMUSER)` |
| 08 | `08-ispf-exit-command.png` | `=X` entered to terminate ISPF |
| 09 | `09-ispf-log-dataset-disposition.png` | ISPF log data set disposition processing |
| 10 | `10-ready-after-ispf-exit.png` | Native `READY` after ISPF termination |
| 11 | `11-native-tso-profile-result.png` | Native TSO `PROFILE` result, again showing `PREFIX(IBMUSER)` |
| 12 | `12-native-tso-logoff.png` | `LOGOFF` entered from native TSO |
| 13 | `13-return-to-adcd-redacted.png` | Return to ADCD/session manager; terminal/network identifier redacted |

## Security review

The source session included information that is unsuitable for a public repository. Publication controls applied to this lab:

- the ADCD screen containing an explicit user/password table was **excluded** from the evidence set;
- the VTAM terminal identifier shown on the ADCD entry screen was **redacted**;
- the IP-address field and terminal/network identification area were redacted together;
- no MAC addresses or host adapter names are included in the published evidence;
- no password entered during the TSO/E logon is visible in the published evidence.

See [`docs/security-review.md`](docs/security-review.md).

## Commands

See [`commands/lab01-commands.txt`](commands/lab01-commands.txt).

## Documentation notes

See [`docs/technical-notes.md`](docs/technical-notes.md).

## References

1. Kurt Bosler, *MVS TSO/ISPF: A Guide for Users and Developers*, System Access: **Accessing TSO** and **Accessing ISPF**. The book describes the TSO `READY` prompt, starting ISPF from TSO, the ISPF hierarchy, and ISPF termination/log-list processing.
2. Franz Lanz, *IBM z/OS ISPF Smart Practices, Volume 1: User's Guide*, Chapter 3 **The TSO/ISPF logon process** and Chapter 4 **Customize ISPF**. Lanz explains the logon procedure, ISPF start, the Primary Option Menu and the possible return to `READY` when ISPF ends.
3. IBM Redbooks, *Introduction to the New Mainframe: z/OS Basics*, Chapter 4 **TSO/E, ISPF, and UNIX: Interactive facilities of z/OS**. Its exercises explicitly use `=X` to leave ISPF for native TSO and `PROFILE` to inspect the prefix.
4. IBM Redbooks, *z/OS Version 1 Release 11 Implementation*, used as release-level context for the laboratory environment and ISPF/TSO/E behavior on z/OS V1R11.
