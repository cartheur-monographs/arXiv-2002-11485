# SOFTSIM Heat-Emergency Prototype

This note turns the paper's bounded example into a small prototype plan you can
build in SOFTSIM IDE.

The goal is not to build a realistic city model on the first pass. The goal is
to build one small stateful advisory simulation that demonstrates the paper's
three reasoning layers:

1. observational: what state is the district likely in now?
2. interventional: what may happen under each available action?
3. counterfactual: after an observed outcome, what might have happened under a
   different action?

## 1. Prototype scope

Build one district first.

Keep the first version limited to:

- one district
- one latent stress state
- four observed signals
- three available actions
- one-step or two-step lookahead

If that works, then expand to multiple districts later.

## 2. Core model

### Latent state

Use one hidden district condition:

- `stable`
- `strained`
- `critical`

This is the main state your advisory logic is trying to estimate.

### Observable inputs

Use four observed variables per time step:

- `temperature_anomaly`
- `grid_load`
- `er_intake`
- `water_disruption`

Suggested first encoding:

- `temperature_anomaly`: `low | medium | high`
- `grid_load`: `low | medium | high`
- `er_intake`: `low | medium | high`
- `water_disruption`: `0 | 1`

This discrete version is easier to debug than continuous values.

### Available actions

Start with three actions:

- `status_quo`
- `open_cooling_centers`
- `reroute_mobile_generators`

You can add more later, but these three are enough to show the architecture.

## 3. What to build in SOFTSIM

Represent the district as a stateful process with:

- current observed variables
- current estimated latent state
- chosen intervention
- next-step outcome
- history log

At each simulation tick:

1. update observed signals
2. estimate current latent state
3. compare actions
4. choose one action
5. simulate next-step outcome
6. store the step in history

## 4. Minimal data structure

You can model the district with a structure like:

```text
DistrictState
  id
  time_step
  observed:
    temperature_anomaly
    grid_load
    er_intake
    water_disruption
  estimated_state
  estimated_state_probs:
    stable
    strained
    critical
  chosen_action
  next_state
  history[]
```

Each history record can store:

```text
HistoryEntry
  time_step
  observed_signals
  estimated_probs
  candidate_action_scores
  chosen_action
  realized_next_state
```

## 5. Observational layer

The first layer estimates:

`P(state | observations)`

You do not need a sophisticated learner for version 1.

Use simple hand-authored conditional weights.

### Example intuition

- high temperature + high grid load + high ER intake -> pushes toward
  `critical`
- medium temperature + medium grid load + medium ER intake -> pushes toward
  `strained`
- low temperature + low grid load + low ER intake + no water disruption ->
  pushes toward `stable`

### Simple rule-based Bayesian table

You can start with priors like:

- `P(stable) = 0.50`
- `P(strained) = 0.35`
- `P(critical) = 0.15`

Then define rough likelihood tables for each observed variable.

Example:

```text
P(temperature_anomaly = high | critical) = 0.70
P(temperature_anomaly = high | strained) = 0.35
P(temperature_anomaly = high | stable)   = 0.10
```

Do that for each observed variable. Then multiply and normalize.

That gives you:

- `P(stable | X)`
- `P(strained | X)`
- `P(critical | X)`

Pick the max-probability state as the estimated district state.

## 6. Interventional layer

The second layer compares actions under the current estimated condition.

This is the main question:

`What happens next if we choose action A now?`

For version 1, use a transition table:

```text
P(next_state | current_estimated_state, action, observations)
```

You do not need to learn this from data yet. Hand-author a plausible transition
matrix.

### Example transition logic

If the district is `critical`:

- `status_quo` keeps it `critical` with high probability
- `open_cooling_centers` increases the chance of moving to `strained`
- `reroute_mobile_generators` helps more when `grid_load` is high

Example sketch:

```text
If state = critical and action = status_quo:
  critical -> 0.80
  strained -> 0.18
  stable   -> 0.02

If state = critical and action = open_cooling_centers:
  critical -> 0.45
  strained -> 0.45
  stable   -> 0.10

If state = critical and action = reroute_mobile_generators
and grid_load = high:
  critical -> 0.35
  strained -> 0.50
  stable   -> 0.15
```

### Action scoring

Give each action a simple score so the simulator can choose between them.

Example objective:

```text
score(action) =
  3 * P(next_state = stable)
+ 1 * P(next_state = strained)
- 4 * P(next_state = critical)
- action_cost
```

Suggested action costs:

- `status_quo = 0`
- `open_cooling_centers = 1`
- `reroute_mobile_generators = 2`

This lets the simulator make nontrivial choices instead of always choosing the
most aggressive intervention.

## 7. Counterfactual layer

The third layer is what makes this more than a dashboard.

After you observe what really happened, ask:

- what if we had taken a different action?

For version 1, this is easy:

1. store the observed signals at time `t`
2. store the action actually taken
3. store the realized next state
4. rerun the transition model for the actions not taken

Example:

- actual action: `reroute_mobile_generators`
- actual outcome: remained `critical`
- counterfactual query: what was the estimated chance that
  `open_cooling_centers` would have moved the district to `strained`?

This can be shown as a simple comparison table:

```text
Observed at t:
  temp=high, grid=high, er=high, water=1

Actual action:
  reroute_mobile_generators

Actual outcome:
  critical

Counterfactual action comparison:
  status_quo               -> P(critical at t+1) = 0.80
  open_cooling_centers     -> P(critical at t+1) = 0.45
  reroute_mobile_generators-> P(critical at t+1) = 0.35
```

That gives you an audit-style advisory explanation.

## 8. Suggested SOFTSIM build order

Build it in this order:

### Stage 1

Create one district object and manually set observations per time step.

Success condition:

- you can run 10 to 20 ticks
- you can see observations changing over time

### Stage 2

Add the observational layer.

Success condition:

- each tick outputs probabilities for `stable`, `strained`, and `critical`

### Stage 3

Add the action comparison table.

Success condition:

- the simulator scores all three actions at each tick

### Stage 4

Add action selection.

Use either:

- highest score wins
- or highest score above a threshold

Success condition:

- the district chooses different actions under different observed conditions

### Stage 5

Add realized next-state transitions.

Success condition:

- the district state evolves over time instead of staying fixed

### Stage 6

Add counterfactual replay for the action not taken.

Success condition:

- each tick can produce a post hoc comparison report

## 9. First useful output screens

If SOFTSIM supports panels or views, build these first:

- `Current district status`
- `Estimated state probabilities`
- `Action comparison`
- `Chosen action`
- `Counterfactual replay`
- `History timeline`

The most important view is the action comparison table. That is where the
paper's argument becomes visible.

## 10. Recommended first scenario set

Create three simple scenarios.

### Scenario A: mild heat day

- temperature: medium
- grid: medium
- ER intake: low
- water disruption: 0

Expected behavior:

- estimated state near `strained`
- `status_quo` or `open_cooling_centers` may be chosen

### Scenario B: severe heat and grid stress

- temperature: high
- grid: high
- ER intake: high
- water disruption: 0

Expected behavior:

- estimated state near `critical`
- intervention should beat `status_quo`

### Scenario C: cascading service disruption

- temperature: high
- grid: high
- ER intake: high
- water disruption: 1

Expected behavior:

- highest critical risk
- counterfactual layer becomes especially important

## 11. What not to do yet

Avoid these on version 1:

- multiple cities
- continuous optimization
- reinforcement learning
- large policy menus
- real-world policy claims
- real hospital or utility data

Those will make the prototype harder to interpret before the architecture is
clear.

## 12. What this prototype proves

If this prototype works, it does not prove that the paper solves governance.

It does show something narrower and useful:

- the three-layer architecture is implementable
- the architecture can be simulated with explicit states and actions
- intervention comparison is clearer than raw monitoring alone
- counterfactual replay can be built into the advisory loop

That is enough for a first SOFTSIM prototype.

## 13. Best next step after version 1

After the one-district prototype works, expand in this order:

1. multiple districts with different local observations
2. shared resource constraints across districts
3. delayed effects over two or three steps
4. policy budget costs
5. human override or approval gate

That will move the prototype closer to the paper's governance setting without
making the first build too large.
