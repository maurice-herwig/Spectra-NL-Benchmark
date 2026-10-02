# Baseball Pitch Clock (Hard)

A baseball pitch clock limits the time between pitches. This task uses a simplified MLB-style pitch-clock model.
The system operates in discrete time steps.
Each time step corresponds to one second of game time.
The controller updates the pitch-clock value and indicates whether a pitcher or batter violation occurs. For this task, assume that at most one timer event occurs in each time step.
The events `newBatter`, `pitchStarted`, and `disengagement` reset the pitch clock as shown in the table below.
After a pitch is started, the ball may be in play. While the ball is in play, the pitch clock must not count down and no pitch-clock violation is signaled.
If no event row applies and the timer is running, the pitch clock decreases by one.

**Environment-Variables:**

- `runnerOnBase`: true if at least one runner is currently on base.
- `newBatter`: true if a new batter is entering the plate appearance.
- `pitcherReady`: true if the pitcher has the ball and the pitch timer should run.
- `batterReady`: true if the batter is in the box and ready for the pitch.
- `pitchStarted`: true if the pitcher has started the pitching motion.
- `ballInPlay`: true if the ball is currently in play after a pitch.
- `timeout`: true if a timeout or other valid interruption occurs.
- `disengagement`: true if the pitcher legally steps off or attempts a pickoff.

**System-Variables:**

- `pitchClock`: integer value in the range `0..30` representing the remaining pitch-clock time in seconds.
- `pitcherViolation`: true if the pitcher violates the pitch clock.
- `batterViolation`: true if the batter violates the pitch clock.

| Event condition | `pitchClock` in the next step | Violation signal |
|---|---|---|
| `newBatter` | set to `30` | none |
| `timeout` | unchanged | none |
| `ballInPlay` | unchanged | none |
| `pitchStarted` and `runnerOnBase` | set to `18` | none |
| `pitchStarted` and not `runnerOnBase` | set to `15` | none |
| `disengagement` and `runnerOnBase` | set to `18` | none |
| `disengagement` and not `runnerOnBase` | set to `15` | none |
| `pitchClock = 8` and not `batterReady` | unchanged | `batterViolation` |
| `pitchClock = 0` and not `pitchStarted` | keep at `0` | `pitcherViolation` |
| normal running step | decrease by `1` | none |
| waiting step | unchanged | none |

*Table: Pitch-clock event table. A normal running step occurs when `pitcherReady` is true and no other event row applies. A waiting step occurs when `pitcherReady` is false and no other event row applies.*

### Hint: Baseball terminology

In baseball, a *pitch* is the throw from the pitcher toward the batter.
The *batter* is the offensive player who tries to hit the ball.
A *runner* is an offensive player who has reached one of the bases.
A *disengagement* means that the pitcher legally steps off the pitching position or attempts to throw the ball to a base instead of pitching to the batter.
A *timeout* is a valid interruption of play.

A typical play starts when the pitcher receives the ball and the batter gets ready.
The pitch clock then counts down until the pitcher starts the pitch.
After the pitch, the ball may be in play, for example if the batter hits it.
While the ball is in play, the pitch clock is not counting down.
Once the play is over and the pitcher is ready for the next pitch, the pitch clock starts counting down again.
