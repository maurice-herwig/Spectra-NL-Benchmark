# Vacuum Cleaner (Medium)

A household cleaning robot can vacuum, mop, or perform both actions at the same time. The robot operates in discrete cleaning steps. One step corresponds to the time between two visits to the charging station. The robot receives information about its current resources and whether cleaning is requested. Based on this information, it must decide whether vacuuming and/or mopping should be active.

**Environment-Variables:**

- `batteryOk`: true if the robot has enough battery charge.
- `freshWaterFull`: true if the fresh-water tank is full.
- `dirtyWaterFull`: true if the dirty-water tank is full.
- `dustBagFull`: true if the vacuum dust bag is full.
- `cleanRequest`: true if the robot is currently requested to clean.

**System-Variables:**

- `vacuum`: true if the robot vacuums during the current step.
- `mop`: true if the robot mops during the current step.

The table below shows selected operating modes of the cleaning robot.
Each row describes one possible valuation of the environment variables and the system variables.
A value of `t` means that the signal is true, a value of `f` means that the signal is false, and `*` means that the value is irrelevant for that row.

| `cleanRequest` | `batteryOk` | `dustBagFull` | `freshWaterFull` | `dirtyWaterFull` | `vacuum` | `mop` |
|---|---|---|---|---|---|---|
| `f` | `*` | `*` | `*` | `*` | `f` | `f` |
| `*` | `f` | `*` | `*` | `*` | `f` | `f` |
| `t` | `t` | `f` | `t` | `f` | `t` | `t` |
| `t` | `t` | `t` | `t` | `f` | `f` | `t` |
| `t` | `t` | `f` | `t` | `t` | `t` | `f` |
| `t` | `t` | `t` | `t` | `t` | `f` | `f` |
| `t` | `t` | `f` | `f` | `t` | `t` | `f` |
| `t` | `t` | `t` | `f` | `t` | `f` | `f` |
| `t` | `t` | `*` | `f` | `f` | `*` | see below |

In addition to the operating modes shown in the table, the highlighted last row describes the special case for the mopping function.
If cleaning is requested, the battery is okay, the fresh-water tank is not full, and the dirty-water tank is not full, the robot must still mop during the current cleaning step.
After this cleaning step, the robot reaches the charging station.
In the immediately following step, the robot must no longer mop as long as the relevant environment variables remain unchanged, i.e., as long as cleaning is still requested, the battery is still okay, the fresh-water tank is still not full, and the dirty-water tank is still not full.
If one of these environment variables changes in the following step, the required value of `mop` is determined again by the table and this special-case rule.
