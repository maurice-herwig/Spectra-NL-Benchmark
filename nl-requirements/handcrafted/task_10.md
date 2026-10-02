# Balcony Power Plant with Storage (Hard)

A balcony power plant supplies electricity to a household and is connected to a battery storage system.
The household also contains a heat pump that can consume additional electricity when heating is required.
The controller decides whether the balcony power plant is active, whether electricity is drawn from the public grid, and whether the heat pump is running.
The goal of the controller is to reduce electricity costs while keeping enough stored energy available for situations in which the balcony power plant cannot be used or additional demand is expected.

To reduce battery wear, the storage should repeatedly return to the medium charge range.
In other words, the system should infinitely often reach situations in which `storageLevel` is `MEDIUM`, whenever this is possible under the environment behavior.

For this task, assume that thunderstorms and cold fronts occur repeatedly over time, but also that there are repeatedly time points at which no thunderstorm and no cold front are present or forecast.

**Environment-Variables:**

- `stormNow`: true if a thunderstorm is currently approaching.
- `stormSoon`: true if a thunderstorm is forecast for the next days.
- `coldNow`: true if cold weather is currently detected.
- `coldFrontSoon`: true if a cold front is forecast for the next days.
- `storageLevel`: current charge level of the battery storage. The possible values are `LOW`, `MEDIUM`, and `HIGH`.
- `priceLow`: true if the current electricity price is low.

**System-Variables:**

- `solarOn`: true if the balcony power plant is active.
- `drawFromGrid`: true if electricity is drawn from the public grid.
- `heatPumpOn`: true if the heat pump is running.

The following rules must hold:

- The balcony power plant must be switched off if a thunderstorm is currently approaching.
  Otherwise, the balcony power plant must be switched on.
- The heat pump must be switched on exactly when cold weather is currently detected.
- Electricity must be drawn from the public grid in the following cases:
  - The storage level is `LOW`, the balcony power plant is off because of a thunderstorm, and the heat pump is running.
  - The storage level is `LOW`, the balcony power plant is off because of a thunderstorm, and a cold front is forecast.
  - A thunderstorm or cold front is forecast, the storage level is not `HIGH`, and the electricity price is low.
  - The storage level is `LOW` and the electricity price is low.
- In all other cases, no electricity must be drawn from the public grid.
