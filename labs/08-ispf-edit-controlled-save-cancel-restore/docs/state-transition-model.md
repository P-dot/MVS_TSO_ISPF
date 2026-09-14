# State Transition Model — Lab 08

## Purpose

Model the difference between the persistent member and the active ISPF Edit working state.

```text
                         +----------------------+
                         |  Known disk baseline |
                         +----------+-----------+
                                    |
                                    v
                           +--------+--------+
                           |  Edit working   |
                           |      state      |
                           +---+----------+--+
                               |          |
                          CANCEL|          |SAVE
                               |          |
                               v          v
                    +----------+--+   +---+----------------+
                    | baseline     |   | changed disk state |
                    | preserved    |   | persisted          |
                    +----------+---+   +---------+----------+
                               |                 |
                               |                 v
                               |        +--------+---------+
                               |        | controlled       |
                               |        | restoration Edit |
                               |        +--------+---------+
                               |                 |
                               |                SAVE
                               |                 |
                               +--------+--------+
                                        |
                                        v
                              +---------+----------+
                              | known disk baseline |
                              | restored            |
                              +---------+----------+
                                        |
                                        v
                              independent BROWSE
                                        |
                                        v
                                      PASS
```

## Transaction A — rollback

```text
Disk: LINE-03-CANCEL-TEST
        |
        v
Edit buffer: LINE-03-CANCELLED-CHANGE
        |
      CANCEL
        |
        v
Disk: LINE-03-CANCEL-TEST
```

## Transaction B — persistence

```text
Disk: LINE-04-SAVE-TEST
        |
        v
Edit buffer: LINE-04-SAVED-CHANGE
        |
       SAVE
        |
        v
Disk: LINE-04-SAVED-CHANGE
        |
 independent Browse
        |
        v
       PASS
```

## Recovery transaction

```text
Disk: LINE-04-SAVED-CHANGE
        |
        v
Edit buffer: LINE-04-SAVE-TEST
        |
       SAVE
        |
        v
Disk: LINE-04-SAVE-TEST
        |
      CANCEL
        |
 independent Browse
        |
        v
canonical baseline restored
```

## Boundary

This lab validates application-level Edit rollback through `CANCEL` and controlled restoration after a persisted `SAVE`.

It does **not** validate ISPF Edit Recovery after session/system failure and does **not** validate `UNDO`; the observed profile had `RECOVERY OFF WARN` and explicitly warned that UNDO was unavailable.
