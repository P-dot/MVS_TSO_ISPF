# MVS TSO/ISPF Labs

Hands-on TSO/E and ISPF laboratories executed on an IBM z/OS 1.11 ADCD environment.

The sequence is documentation-led and Architecture V2 governed.

## Labs

Labs 01–13 remain previously validated.

| Lab | Topic | Status |
|---|---|---|
| [14](labs/14-ispf-edit-primary-commands/) | ISPF Edit primary commands: HEX, FIND, LOCATE and RESET | ✅ Completed |

## Repository-owned Edit fixtures

```text
IBMUSER.ISPF.LAB
```

Canonical fixtures are preserved under:

```text
fixtures/edit/
```

Current sequence includes:

```text
EDIT08
EDIT09
EDIT10
EDIT11
EDIT12
EDIT13
EDIT14
```

## Architecture V2 progression

```text
TSO/E
  -> ISPF navigation
  -> Browse
  -> controlled Edit lifecycle
  -> INSERT / DELETE
  -> Repeat / Copy / Move / A / B
  -> MASK / OVERLAY / COLS
  -> BNDS / column shifting / data shifting
  -> EXCLUDE / labels / TABS display state
  -> Edit primary commands
  -> Advanced Edit primary commands
```

## Engineering boundary

`SUBMIT` is introduced by the source chapter but is intentionally not executed in this standalone repository lab.

Its execution belongs to a later cross-repository path:

```text
ISPF -> JCL -> JES2
```

## Publication security

Evidence was reviewed before publication. No credentials, private network information, tokens, keys or host-side network identifiers are intentionally published.
