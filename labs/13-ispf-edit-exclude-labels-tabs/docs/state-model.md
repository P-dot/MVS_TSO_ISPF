# State Model — Lab 13

Lab 13 deliberately separates four kinds of state.

```text
1. Persistent dataset state
   IBMUSER.ISPF.LAB(EDIT13)

2. Display state
   visible vs excluded records

3. Session positioning state
   user labels and built-in labels

4. Special-line display state
   =TABS>
```

## EXCLUDE invariant

```text
X / X3 / XX
      |
      v
display changes
      |
      v
dataset record remains present
```

`RESET` returns the display to the full working set.

## Label invariant

```text
user label
   |
   v
stored in Edit session / line-command area
   |
   v
LOCATE can position to it
```

The label is not inserted into the dataset record.

`RESET LABEL` clears the session labels.

## TABS invariant

```text
TABS line command
      |
      v
=TABS> special line
```

The lab inspects the existing state only. It does not configure advanced tab semantics.

`RESET SPECIAL` removes the special line.

## Final invariant

```text
persistent_record_count == 18
persistent_content == fixtures/edit/EDIT13-baseline.txt
final_state == BASELINE UNCHANGED
```
