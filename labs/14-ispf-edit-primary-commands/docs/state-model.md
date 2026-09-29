# State Model — Lab 14

Lab 14 validates independent Edit state domains:

```text
display representation
  -> HEX

search scope
  -> X / NX
  -> BNDS

positioning
  -> LOCATE line / built-in labels / state classes

pending line-command state
  -> COMMAND

special-line state
  -> SPECIAL

excluded-line state
  -> EXCLUDED
```

Selective RESET proves these state classes can be cleared independently:

```text
RESET COMMAND
RESET SPECIAL
RESET EXCLUDED
```

Final invariant:

```text
persistent_record_count == 18
persistent_content == fixtures/edit/EDIT14-baseline.txt
BNDS == default/pre-lab state
```
