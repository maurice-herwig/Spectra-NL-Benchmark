# Self-Checkout Assistance (Medium)

A supermarket has five self-checkout stations.
At each station, a customer can request help, and some requests can require an age check.
The controller decides which self-checkout station is assisted during the current step.
A staff member reports in each step whether they are available or unavailable.
Only if a staff member reports being available can the controller assign assistance.
The staff member can assist at most one self-checkout station in each step.

**Environment-Variables:**

- `helpRequest[5]`: `helpRequest[i]` is true if self-checkout station `i` currently requests help.
- `ageCheck[5]`: `ageCheck[i]` is true if self-checkout station `i` currently requires an age check.
- `employeeAvailable`: true if a staff member currently reports being available; false if the staff member currently reports being unavailable.

**System-Variables:**

- `assist[5]`: `assist[i]` is true if self-checkout station `i` is assisted during the current step.

The self-checkout stations are indexed by `0`, `1`, `2`, `3`, and `4`.
The following rules must hold:

- If the staff member reports being unavailable, no self-checkout station may be assisted; in this case all `assist[i]` values must be false.
- If a staff member is available, at most one self-checkout station may be assisted in the same step.
- A self-checkout station may only be assisted if it currently requests help.
- Age-check requests must always be preferred over normal help requests: if at least one age-check request exists and a staff member is available, then the assisted station must be one of the stations requiring an age check.
- If a self-checkout station is assisted in the current step, its help request is automatically cleared in the next step.
