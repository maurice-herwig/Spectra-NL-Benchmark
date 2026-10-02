# Coffee Machine (Medium)

A coffee machine can be switched on and off, prepare coffee, and run an internal cleaning cycle.
The machine uses sensors to observe whether the required resources are available.
The machine state transitions of the coffee machine are shown in the state overview below.
The specification should capture the behavior shown in the overview using the variables listed below.
If an operation is requested but one of its required resource conditions is not satisfied, the status light must be on. Otherwise, the status light must be off.

## State overview for the coffee machine

The machine has the states `OFF`, `READY`, `NEEDS_CLEANING`, `CLEANING_TO_READY`, `CLEANING_TO_OFF`, `MAKING_COFFEE`, and `COFFEE_PENDING`.

The following transitions describe how `machineState` changes:

| From | Condition | To |
|---|---|---|
| `OFF` | `powerButton` | `NEEDS_CLEANING` |
| `NEEDS_CLEANING` | `waterFull` and `dripTrayEmpty` | `CLEANING_TO_READY` |
| `CLEANING_TO_READY` | after cleaning | `READY` |
| `READY` | `powerButton` and `waterFull` and `dripTrayEmpty` | `CLEANING_TO_OFF` |
| `CLEANING_TO_OFF` | after cleaning | `OFF` |
| `READY` | `coffeeButton` and `waterFull` and `beansFull` | `MAKING_COFFEE` |
| `MAKING_COFFEE` | after coffee | `READY` |
| `READY` | `coffeeButton` and (missing water or beans) | `COFFEE_PENDING` |
| `COFFEE_PENDING` | `waterFull` and `beansFull` | `MAKING_COFFEE` |
| `NEEDS_CLEANING` | missing water or tray not empty | `NEEDS_CLEANING` (self-loop) |
| `READY` | `powerButton` and (missing water or tray not empty) | `READY` (self-loop) |
| `COFFEE_PENDING` | missing water or beans | `COFFEE_PENDING` (self-loop) |

The self-loops indicate that the machine remains in the current state while required resources are missing.

**Environment-Variables:**

- `waterFull`: true if the water tank is full.
- `dripTrayEmpty`: true if the drip tray is empty.
- `beansFull`: true if the bean container is full.
- `powerButton`: true if the power button is pressed.
- `coffeeButton`: true if the coffee button is pressed.

**System-Variables:**

- `machineState`: current state of the machine. The possible values are `OFF`, `READY`, `NEEDS_CLEANING`, `CLEANING_TO_READY`, `CLEANING_TO_OFF`, `MAKING_COFFEE`, and `COFFEE_PENDING`.
- `statusLight`: true if the machine indicates that user action is required.
