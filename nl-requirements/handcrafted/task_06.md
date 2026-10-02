# Ski Lift Entry (Medium)

A ski lift has entry gates that control when skiers may move forward to enter the next chair.
The controller also determines the speed at which the chair approaches the entry area. The system operates in discrete decision steps.
In each step, the controller decides whether the gates should open in the next step and which lift speed should be used in the next step.
A separate sensor indicates whether a chair will be at the boarding position in the next step.

**Environment-Variables:**

- `sensor20cm`: true if the lower gate sensor is active.
- `sensor130cm`: true if the upper gate sensor is active.
- `entryOccupied`: true if a skier is currently detected in the entry area.
- `chairApproaching`: true if a chair will be at the boarding position in the next step.
- `emergencyStop`: true if the emergency stop button is currently active.

**System-Variables:**

- `gatesOpen`: true if the entry gates are open.
- `liftSpeed`: the speed of the lift. The possible values are `OFF`, `SLOW`, and `FAST`.

The rules are grouped by priority. A rule only applies if no rule from a higher priority level applies.

### Priority 1: Emergency stop

If the emergency stop is active, the lift must be stopped in the next step. The entry gates must keep their current position and must not change while the emergency stop remains active.

### Priority 2: Occupied entry area

If the entry area is occupied by a skier, the gates must not open in the next step. The lift speed must be set to `SLOW` in the next step.

### Priority 3: No chair approaching

If no chair is approaching the boarding position, the gates must not open in the next step. The lift speed must be set to `SLOW` in the next step.

### Priority 4: Adult skiers detected

If both gate sensors are active, this indicates that adult skiers are waiting. The gates must open in the next step, and the lift speed must be set to `FAST` in the next step.

### Priority 5: At least one child skier detected

If only the lower gate sensor is active, this indicates that at least one child skier is waiting. The gates must open in the next step, and the lift speed must be set to `SLOW` in the next step.

### Priority 6: No valid skier group detected

If no gate sensor is active, or if only the upper gate sensor is active, the gates must not open in the next step. The lift speed must be set to `SLOW` in the next step.
