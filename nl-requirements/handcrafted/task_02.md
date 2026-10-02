# Smart Door Lock (Easy)

A smart door lock controls access to a restricted room.
The door can detect whether a person is standing in front of it, whether the presented access badge is valid, and whether the door is currently closed.
The controller decides whether the door is unlocked and whether an alarm is active.
An emergency unlock mode can be activated to allow access independently of the badge reader.

**Environment-Variables:**

- `personDetected`: true if a person is detected in front of the door.
- `badgeValid`: true if the presented access badge is valid.
- `doorClosed`: true if the door is currently closed.
- `emergencyUnlock`: true if emergency unlocking is currently active.

**System-Variables:**

- `doorUnlocked`: true if the door is unlocked.
- `alarm`: true if the alarm is active.

The table below shows selected operating modes of the smart door lock. Each row describes one possible valuation of the environment variables and the corresponding system variables.
A value of `t` means that the signal is true, a value of `f` means that the signal is false, and `*` means that the value is irrelevant for that row.

| `emergencyUnlock` | `personDetected` | `badgeValid` | `doorClosed` | `doorUnlocked` | `alarm` |
|---|---|---|---|---|---|
| `t` | `*` | `*` | `*` | `t` | `f` |
| `f` | `t` | `f` | `f` | `f` | `t` |
| `f` | `t` | `t` | `*` | `t` | `f` |
| `f` | `t` | `f` | `t` | `f` | `t` |
| `f` | `f` | `*` | `*` | `f` | `f` |

*Table: Selected operating modes of the smart door lock.*
