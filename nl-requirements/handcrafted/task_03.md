# Railroad Crossing (Easy)

A railroad crossing controls the barriers for cars and the stop signal for approaching trains.
If the stop signal is active, an approaching train must stop before reaching the crossing.
The train-approach sensor is placed far enough away from the crossing so that a train can still stop when the stop signal is active.

**Environment-Variables:**

- `carOnCrossing`: true if a car is currently on the railroad crossing.
- `trainApproaching`: true if a train is currently approaching the railroad crossing.
- `trainPassed`: true if the last detected train has completely passed the railroad crossing.

**System-Variables:**

- `barrierClosed`: true if the barriers for cars are closed.
- `trainStopSignal`: true if the stop signal for approaching trains is active.

The rules are grouped by priority. A rule only applies if no rule from a higher priority level applies.

### Priority 1: Car on crossing

If a car is on the railroad crossing, the barriers for cars must not close. The stop signal for approaching trains must be active.

### Priority 2: Train approaching

If a train is approaching and no car is on the railroad crossing, the barriers for cars must close. The stop signal for approaching trains must be inactive.

### Priority 3: Train passed

If the last detected train has passed the railroad crossing and no new train is approaching, the barriers for cars must open and the stop signal for approaching trains must be active.
