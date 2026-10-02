# E-Scooter Rental (Hard)

An e-scooter rental app manages the state of a scooter and decides when the control center must be informed about the scooter battery.
The system operates in discrete decision steps.

**Environment-Variables:**

- `reservationRequest`: true if a user currently requests the scooter.
- `riding`: true if the scooter is currently being ridden.
- `chargingStarted`: true if the scooter is placed on a charger.
- `batteryLevel`: current battery level of the scooter. The possible values are `LOW`, `MEDIUM`, and `HIGH`.

**System-Variables:**

- `scooterState`: current state of the scooter in the rental system. The possible values are `FREE`, `RESERVED`, `RIDING`, and `CHARGING`.
- `availableForRental`: true if the scooter is available for new reservations.
- `notifyCenter`: true if the control center is notified.

The following assumptions about the environment can be made:

- The scooter is placed on a charger repeatedly over time.
- Whenever the scooter is charging, the battery level eventually reaches `HIGH`.

## State transitions of the e-scooter rental system

| From | Condition | To |
|---|---|---|
| `FREE` | `reservationRequest` and `batteryLevel != LOW` and `!chargingStarted` | `RESERVED` |
| `RESERVED` | `riding` and `!chargingStarted` | `RIDING` |
| `RIDING` | `!riding` and `!chargingStarted` | `FREE` |
| `FREE` | `chargingStarted` | `CHARGING` |
| `RESERVED` | `chargingStarted` | `CHARGING` |
| `RIDING` | `chargingStarted` | `CHARGING` |
| `CHARGING` | `batteryLevel = HIGH` | `FREE` |
| `FREE` | otherwise | `FREE` (self-loop) |
| `RESERVED` | `!riding` and `!chargingStarted` | `RESERVED` (self-loop) |
| `RIDING` | `riding` and `!chargingStarted` | `RIDING` (self-loop) |
| `CHARGING` | `batteryLevel != HIGH` | `CHARGING` (self-loop) |

Initially, the scooter state is `FREE`. The scooter is available for rental exactly when `scooterState` is `FREE` and `batteryLevel` is not `LOW`.
The state transitions of `scooterState` are shown in the table above.
The transition to `CHARGING` has priority whenever `chargingStarted` is true.

The following notification rules must also hold:

- If the scooter state is `CHARGING`, no notification must be sent to the control center.
- If the scooter is not charging and the battery level changes from `HIGH` to `MEDIUM`, one notification must be sent to the control center.
- While the scooter is not charging and the battery level is `LOW`, a notification must be sent to the control center in every step.
- In all other cases, no notification must be sent to the control center.
