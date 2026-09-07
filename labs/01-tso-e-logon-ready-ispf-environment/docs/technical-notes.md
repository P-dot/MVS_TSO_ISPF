# Technical Notes — Lab 01

## TSO/E and ISPF are separate layers

TSO/E provides the interactive z/OS user session and native command environment. ISPF is invoked within that environment and provides the full-screen menu/panel interface.

The laboratory demonstrated this directly by running `PROFILE` from the ISPF Command Shell, terminating ISPF, reaching `READY`, and running `PROFILE` again.

## The READY prompt

`READY` indicates that the TSO command environment is available to accept another command. In the captured environment, `READY` appeared after ISPF terminated, proving that the TSO/E session remained active.

## PROFILE and PREFIX

The `PROFILE` output inside ISPF and in native TSO both contained:

```text
PREFIX(IBMUSER)
```

The prefix is important because it affects how TSO resolves non-fully-qualified data set names. Detailed data set naming behavior is intentionally deferred to later labs.

## ISPF Command Shell

ISPF option 6 provides a Command Shell for TSO or workstation commands. It does not create a separate TSO user session; this lab demonstrated that it uses the active TSO/E context.

## ISPF termination and SPFLOG

When `=X` was used, the environment displayed the ISPF log-data-set disposition panel and kept:

```text
IBMUSER.SPFLOG1.LIST
```

The extra disposition panel is consistent with ISPF log/list processing when termination defaults do not suppress it or when data set processing requires confirmation.

## Observed logon-procedure naming difference

The TSO/E LOGON panel displayed:

```text
DBSPROC9
```

while the ISPF Primary Option Menu displayed:

```text
DBSPROC
```

The cause is not established by the evidence collected in Lab 01. It is therefore recorded as an observation rather than explained by assumption.

## Return codes

This was an interactive TSO/ISPF lab. No JCL job was submitted, so there is no JES step completion code and `RC=0000` is not applicable.
