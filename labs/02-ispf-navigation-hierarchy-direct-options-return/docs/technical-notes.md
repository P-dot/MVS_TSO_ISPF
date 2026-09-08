# Technical Notes — Lab 02

## ISPF hierarchy

The observed ISPF environment exposes the standard idea of hierarchical selection panels. In this lab, option `3` opened the Utility Selection Panel and suboption `4` opened the Data Set List Utility.

The hierarchy observed was:

```text
Primary Option Menu
        |
        +-- 3 Utilities
              |
              +-- 4 Dslist
```

## Direct option entry

Entering:

```text
3.4
```

from the Primary Option Menu reached the same Data Set List Utility without displaying the intermediate Utility Selection Panel.

The key point is that the route identifies the option and suboption together.

## Jump function

Entering:

```text
=3.4
```

from the Edit Entry Panel moved directly to the Data Set List Utility.

The leading equals sign is what distinguishes the jump request from normal local selection.

This matters operationally because it avoids manually ending the current function, returning through menus and then navigating down another branch.

## F3 and END

In the observed session, `F3` returned from the Data Set List Utility to the Utility Selection Panel.

This is consistent with normal ISPF use where PF3 is mapped to `END`.

The lab treats `F3 / END` together because the practical behavior being demonstrated is ending the current function and returning to the previous level.

## RETURN

Entering:

```text
RETURN
```

from the Data Set List Utility returned directly to the ISPF Primary Option Menu.

This creates a useful distinction:

```text
F3 / END  -> previous level
RETURN    -> Primary Option Menu
```

## Why this matters

For a new ISPF user, menu-by-menu navigation is useful because it reveals the structure of the product.

For daily work, direct paths and jump commands reduce repeated navigation and make the interface faster to use.

These techniques also prepare the ground for later labs involving:

- multiple logical screens,
- command tables,
- REXX,
- ISPF services,
- edit macros,
- and task automation.
