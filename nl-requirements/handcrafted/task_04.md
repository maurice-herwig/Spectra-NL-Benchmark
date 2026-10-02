# Restaurant Table Assignment (Easy)

A restaurant decides how to handle arriving guest groups.
A group may arrive with or without a reservation.
Depending on table availability, kitchen status, and group size, the restaurant either seats the group, asks it to wait, declines it, or does nothing if no group is currently arriving.

Assume that guest groups keep arriving repeatedly over time.
Also assume that tables become available repeatedly over time, because guests eventually finish their meals and leave.

**Environment-Variables:**

- `groupArrives`: true if a new guest group is currently arriving.
- `reservation`: true if the arriving group has a reservation.
- `tableAvailable`: true if at least one suitable table is currently available.
- `kitchenOpen`: true if the kitchen is currently open.
- `groupTooLarge`: true if the arriving group is too large for the restaurant.

**System-Variables:**

- `decision`: current decision of the restaurant. The possible values are `NONE`, `SEAT`, `WAIT`, and `DECLINE`.

The following assumptions about the environment can be made:

- Guest groups arrive repeatedly over time.
- Tables become available repeatedly over time.

The table below shows the restaurant's decision for the possible operating situations.
A value of `t` means that the signal is true, a value of `f` means that the signal is false, and `*` means that the value is irrelevant for that row.

| `groupArrives` | `kitchenOpen` | `groupTooLarge` | `tableAvailable` | `reservation` | `decision` |
|---|---|---|---|---|---|
| `f` | `*` | `*` | `*` | `*` | `NONE` |
| `t` | `f` | `*` | `*` | `*` | `DECLINE` |
| `t` | `t` | `t` | `*` | `*` | `DECLINE` |
| `t` | `t` | `f` | `t` | `*` | `SEAT` |
| `t` | `t` | `f` | `f` | `t` | `WAIT` |
| `t` | `t` | `f` | `f` | `f` | `DECLINE` |

*Table: Decision table for the restaurant table assignment.*
