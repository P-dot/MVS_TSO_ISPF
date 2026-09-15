# Record-Count State Model — Lab 09

```text
INSERT:
13 -> I -> 14 -> I3 -> 17 -> CANCEL -> 13 persistent

DELETE:
13 -> D -> 12 -> D3 -> 9
                     |
                     +-> DD pending -> RESET -> 9
                     |
                     +-> DD/DD -> 6 -> CANCEL -> 13 persistent
```

Acceptance invariant:

```text
persistent_record_count == 13
persistent_content == fixtures/edit/EDIT09-baseline.txt
```
