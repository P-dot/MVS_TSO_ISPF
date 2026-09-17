# MVS TSO/ISPF Labs

Hands-on TSO/E and ISPF laboratories executed on an IBM z/OS 1.11 ADCD environment.

The sequence is documentation-led. Kurt Bosler's *MVS TSO/ISPF: A Guide for Users and Developers* is the main historical/didactic source, complemented by Franz Lanz and IBM documentation.

## Labs

| Lab | Topic | Status |
|---|---|---|
| [01](labs/01-tso-e-logon-ready-ispf-environment/) | TSO/E logon, native READY mode and ISPF environment | ✅ Completed |
| [02](labs/02-ispf-navigation-hierarchy-direct-options-return/) | ISPF hierarchy, direct option entry, jump function and RETURN | ✅ Completed |
| [03](labs/03-ispf-split-screen-swap-logical-screens/) | ISPF logical screens, SPLIT, SWAP and task-list validation | ✅ Completed |
| [04](labs/04-ispf-dataset-names-member-lists/) | Data set naming, DSLIST and member-list processing | ✅ Completed |
| [05](labs/05-ispf-browse-navigation-scrolling-locate-labels/) | ISPF Browse navigation, scrolling, LOCATE and labels | ✅ Completed |
| [06](labs/06-ispf-browse-display-hex-recursive/) | ISPF Browse display controls, hexadecimal representation and recursive Browse | ✅ Completed |
| [07](labs/07-ispf-browse-find-rfind-search-controls/) | ISPF Browse FIND, RFIND and search controls | ✅ Completed |
| [08](labs/08-ispf-edit-controlled-save-cancel-restore/) | Controlled ISPF Edit lifecycle: SAVE, CANCEL, persistence and restore | ✅ Completed |
| [09](labs/09-ispf-edit-insert-delete-line-commands/) | ISPF Edit line commands: controlled INSERT and DELETE | ✅ Completed |
| [10](labs/10-ispf-edit-repeat-copy-move-before-after/) | ISPF Edit Repeat, Copy, Move, Before/After and multiple-command handling | ✅ Completed |
| [11](labs/11-ispf-edit-mask-overlay-cols/) | ISPF Edit MASK, OVERLAY and column indicators | ✅ Completed |
| [12](labs/12-ispf-edit-bnds-column-data-shifting/) | ISPF Edit BNDS, column shifting and data shifting | ✅ Completed |

## Repository-owned Edit fixtures

State-changing ISPF labs use:

```text
IBMUSER.ISPF.LAB
```

Canonical fixtures are preserved under:

```text
fixtures/edit/
```

Current sequence:

```text
EDIT08
EDIT09
EDIT10
EDIT11
EDIT12
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
  -> EXCLUDE / Edit labels / TABS
  -> Edit primary commands
  -> REXX / ISPF automation prerequisites
```

## Publication security

Evidence is reviewed before publication. Credentials, private network information, tokens, keys and host-side network identifiers are not intentionally published.
