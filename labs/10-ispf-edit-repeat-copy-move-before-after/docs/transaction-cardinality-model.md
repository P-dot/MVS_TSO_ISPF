# Transaction and Cardinality Model — Lab 10

## REPEAT

```text
28
 |
 R
 v
29
 |
 R3
 v
32
 |
 RR/RR
 v
34
 |
 CANCEL
 v
28 persistent
```

## COPY

```text
28
 |
 C + A
 v
29
 |
 C2 + B
 v
31
 |
 CC/CC + A
 v
33
 |
 CANCEL
 v
28 persistent
```

COPY preserves source records.

## MOVE

```text
28
 |
 M + B
 v
28
 |
 M2 + A2
 v
30
 |
 MM/MM + B
 v
30
 |
 CANCEL
 v
28 persistent
```

MOVE removes the source from its original position.

`A2` repeats the moved payload twice at the destination and therefore changes cardinality.

## Multiple-command negative and corrected paths

```text
R + C/A + M/B
      |
      v
Command conflict
      |
   CANCEL
      |
      v
28 persistent
```

Corrected:

```text
R + C/A
   |
ONE ENTER
   |
   v
30 working
   |
CANCEL
   |
   v
28 persistent
```

## Final invariant

```text
persistent_record_count == 28
persistent_content == fixtures/edit/EDIT10-baseline.txt
```
