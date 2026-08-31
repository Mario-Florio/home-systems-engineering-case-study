# Home Systems Simulation Design

**Contents:**

- [Home Systems Simulation Design](#home-systems-simulation-design)
  - [Purpose](#purpose)
  - [1. Simulation Scope](#1-simulation-scope)
  - [2. Simulation Abstraction](#2-simulation-abstraction)
    - [2.1. Resource Normalization](#21-resource-normalization)
        - [Example](#example)
    - [2.2. Demand and Storage](#22-demand-and-storage)
    - [2.3. Time](#23-time)
  - [3. Subsystem Representation](#3-subsystem-representation)
    - [3.1. Functional Abstraction](#31-functional-abstraction)
    - [3.2. Implicity Implementation Behavior](#32-implicit-implementation-behavior)
  - [4. Scenarios](#4-scenarios)
    - [4.1. Definition](#41-definition)
        - [Example](#example-1)
    - [4.2. Scenario Design Principle](#42-scenario-design-principle)
    - [4.3. Deterministic Scenarios](#43-deterministic-scenarios)
  - [5. Modes](#5-modes)
    - [5.1. Definition](#51-definition)
    - [5.2. Distinguishing Modes from Scenarios](#52-distinguishing-modes-from-scenarios)
    - [5.3. Development and Degradation](#53-development-and-degradation)
  - [6. Dynamic and Static Variables](#6-dynamic-and-static-variables)
  - [7. System Performance Parameters](#7-system-performance-parameters)
  - [8. Simulation Runs](#8-simulation-runs)
  - [9. Simulation Reporting](#9-simulation-reporting)
    - [9.1. Primary Effectiveness Measures](#91-primary-effectiveness-measure)
    - [9.2. Contextual Reporting](#92-contextual-reporting)
  - [10. Interpreting Simulation Results](#10-interpreting-simulation-results)
  - [11. From Simulation Results to Operational Requirements](#11-from-simulation-results-to-operational-requirements)
  - [12. Example Requirement Derivation](#12-example-requirement-derivation)
  - [13. Design Principles for Scenario and Mode Crafters](#13-design-principles-for-scenario-and-mode-crafters)
  - [14. Overall Simulation Design](#14-overall-simulation-design)

---

## Purpose

This document defines the conceptual design of the Home Systems simulation used during **Needs Validation**. It is intended to:

* instruct scenario and mode crafters in constructing simulation runs,
* provide a common framework for interpreting simulation behavior and results, and
* document the design and abstraction of the simulation itself.

The simulation is an implementation of an **effectiveness model** for the Home Systems candidate concept. Its purpose is not to reproduce a particular physical implementation, but to evaluate system-level operational behavior across a representative range of conditions.

The simulation therefore remains deliberately abstract. Resources are normalized rather than represented in concrete physical units, and subsystems remain implementation/technology agnostic. The model represents the functional behavior required to evaluate system effectiveness at the current level of system materialization.

---

## 1. Simulation Scope

The Home Systems model represents the household as a collection of interacting resource domains and subsystems.

The principal resource domains may include:

* Food
* Water
* Electricity
* Conditioned climate
* Capital
* Other domains as required by the Home Systems model

The system is modeled primarily as a set of **dynamic resource capacities**. Subsystem behaviors transform resource states over time according to defined relationships.

The simulation is intended to answer questions such as:

* Does the candidate Home System remain feasible under a given operating condition?
* How long can the system maintain self-sufficiency?
* Which resources become limiting?
* Which subsystem produces a bottleneck or failure?
* Which subsystems compete for the same resources?
* Under what environmental conditions does a subsystem's performance become inadequate?
* What compensating capability is necessary for the system to maintain an acceptable operational outcome?

The simulation is not intended at this stage to determine a particular physical implementation. It instead establishes the system-level behavior that a future implementation must be capable of producing.

---

## 2. Simulation Abstraction

### 2.1 Resource Normalization

Resources are represented using normalized values rather than concrete physical units.

Each resource domain establishes an explicit, independent **normalization basis**. The normalization basis is not itself derived from a domain state such as maximum storage or total demand. Instead, it provides the numerical reference against which the domain's resource quantities are represented.

The normalization basis is therefore a property of the simulation model rather than a property derived from the current state of the domain. The particular numerical value used for the basis is an implementation detail; its purpose is to provide a consistent reference scale for normalized resource quantities.

Producer efficiency is normalized separately from resource quantities. The principal producer for a domain has a production efficiency in the range `[0,1]`, where:

`PRODUCER_EFFICIENCY = 1`

represents production sufficient to meet the **total demand of the domain** under adequate environmental conditions. Thus, for the food domain, a principal food-producing subsystem with an efficiency of `1` produces enough food to meet inhabitant demand and the demand of any subsystems that rely upon the food domain.

This allows producer efficiency to have a consistent semantic interpretation across domains without tying the efficiency value to the domain's storage capacity or another derived resource quantity.

#### Example

A food domain may define:

```text
NORMALIZATION_BASIS          # Independent normalization basis
INHABITANT_DEMAND            # [0,∞)
SUBSYSTEM_DEMAND             # [0,∞)
PRODUCER_EFFICIENCY          # [0,1]
SYSTEM_ENVIRONMENT_EFFICACY  # [0,1]
```

These variables are used to derive the domain's capacity, consumption, and production behavior.

For example:

```text
CAPACITY = INITIAL_STOCK / NORMALIZATION_BASIS

INHABITANT_CONSUMPTION_RATE = INHABITANT_DEMAND

OVERALL_CONSUMPTION_RATE =
    INHABITANT_DEMAND + SUBSYSTEM_DEMAND

PRODUCTION_RATE =
    PRODUCER_EFFICIENCY
    * DOMAIN_TOTAL_DEMAND
    * SYSTEM_ENVIRONMENT_EFFICACY
```

The exact transformations may differ between resource domains. The important requirement is that the transformations within each domain share a defined normalization basis and that producer efficiency retains the semantic meaning defined above.

### 2.2 Demand and Storage

Resource behavior is substantially determined by the relationship between demand and available capacity.

Because the normalization basis is independent of domain state, demand and storage may vary without redefining the numerical scale of the domain.

For example, a food normalization basis may be established independently of the household's actual storage capacity. The model can then represent different household demands and storage capacities against that fixed reference.

The simulation designer must therefore define the semantic meaning of normalized values rather than treating them as arbitrary percentages.

A normalized quantity should have an interpretable relationship to:

* demand,
* capacity,
* production,
* consumption,
* storage, and
* time.

### 2.3 Time

The simulation operates over discrete time increments ("ticks"). Scenario and model designers must establish the temporal meaning of a tick and ensure that rates, capacities, and state changes are interpreted consistently.

A rate such as:

`PRODUCTION_RATE = 0.5`

has no complete meaning without a defined temporal basis.

The time basis must therefore be considered whenever a scenario or model parameter is defined, particularly when deriving requirements concerning storage duration, recovery time, production rates, or sustained operation.

---

## 3. Subsystem Representation

### 3.1 Functional Abstraction

Subsystems remain implementation and technology agnostic.

A subsystem is represented by the function it performs rather than by the technology used to implement it.

For example:

`PRODUCE_FOOD`

is preferred at this stage to an implementation-specific representation such as:

`AGRICULTURAL_GARDEN`

The purpose of this abstraction is to evaluate the functional behavior required from a subsystem before selecting or developing a particular physical implementation.

### 3.2 Implicit Implementation Behavior

Although subsystems are implementation agnostic, their behavior must still be represented mathematically.

For example, a candidate food-production function may be represented as:

```text
PRODUCE_FOOD:

FOOD_CAPACITY +=
    PRODUCE_FOOD_EFFICIENCY
    * CLIMATE_EFFICACY
    * GEOGRAPHY_EFFICACY
```

> **Disclaimer:** The above implementation is demonstrative, not prescriptive.

This allows the simulation designer to represent an agricultural implementation implicitly:

`PRODUCE_FOOD_EFFICIENCY = 1`

where `1` represents production sufficient to meet total food-domain demand under adequate environmental conditions, without requiring the simulation to model the physical details of agriculture.

Environmental conditions can then modify the function:

```text
CLIMATE_EFFICACY
GEOGRAPHY_EFFICACY
```

For example, a drought scenario may reduce climate efficacy while leaving geographic efficacy unchanged.

This produces the desired causal relationship:

```text
Environment
    ↓
Subsystem behavior
    ↓
Resource transformation
    ↓
System state
    ↓
Operational outcome
```

---

## 4. Scenarios

### 4.1 Definition

A **scenario** represents a deterministic operational situation imposed on the system from outside the system model being observed for operational outcomes.

Scenarios primarily represent the **operational environment**.

Examples include:

* normal precipitation,
* drought,
* unusually high household demand,
* unusually low precipitation,
* seasonal conditions,
* unfavorable geographic conditions,
* other environmental or externally imposed conditions.

A scenario should describe the condition being imposed rather than unnecessarily encoding the system's response to that condition.

#### Example

A drought should preferably be represented as:

```text
DROUGHT:

CLIMATE_EFFICACY = LOW
```

rather than:

```text
DROUGHT:

FOOD_PRODUCTION = LOW
```

The former represents an environmental condition and allows the candidate system to determine its own response. The latter prematurely specifies the system response.

### 4.2 Scenario Design Principle

Scenarios should represent conditions to which the Home System must respond.

The scenario should therefore avoid prescribing the operational outcome that it is intended to evaluate.

The desired relationship is:

```text
Scenario
    ↓
Environmental / external conditions
    ↓
Candidate system behavior
    ↓
Operational outcome
```

rather than:

```text
Scenario
    ↓
Predetermined system failure
```

### 4.3 Deterministic Scenarios

For the current simulation design, scenarios are deterministic.

A deterministic scenario specifies how relevant external conditions behave over the simulation period. This permits repeatable runs and makes causal interpretation of results possible.

Examples:

```text
NORMAL_SEASON
DROUGHT
SHORT_HARVEST_SEASON
NO_HARVEST_SEASON
HIGH_DEMAND
```

The simulation may later be extended to incorporate more complex or stochastic conditions if required by subsequent analysis.

---

## 5. Modes

### 5.1 Definition

Modes represent conditions in which the system itself is operating.

Kossiakoff distinguishes operational and non-operational modes. Non-operational modes can include activities such as transportation, storage, and maintenance.

For the current Needs Validation simulation, the primary focus is on operational behavior. However, modes may also be useful for representing system conditions that alter subsystem behavior over time.

### 5.2 Distinguishing Modes from Scenarios

A useful distinction is:

**Scenario:** What situation is the system operating within?

**Mode:** What condition is the system operating in?

For example:

```text
SCENARIO = DROUGHT
MODE     = NORMAL_OPERATION
```

could represent a normally operating Home System during a drought.

Alternatively:

```text
SCENARIO = DROUGHT
MODE     = DEVELOPMENT
```

could represent a Home System whose food-production capability is being incrementally developed while simultaneously experiencing drought conditions.

### 5.3 Development and Degradation

Subsystem performance changes that arise from the condition or evolution of the system may be represented as modes.

For example:

```text
DEVELOPMENT MODE

Year 1:
    PRODUCER_EFFICIENCY = 0.6

Year 2:
    PRODUCER_EFFICIENCY = 0.7

Year 3:
    PRODUCER_EFFICIENCY = 0.8
```

Similarly, degraded operation may represent a subsystem whose performance has declined.

The distinction should be based on whether the change represents an external operating condition or a state/condition of the system itself.

| Condition                      | Likely representation |
| ------------------------------ | --------------------- |
| Drought                        | Scenario              |
| High household demand          | Scenario              |
| Poor geographic conditions     | Scenario              |
| Subsystem degradation          | Mode                  |
| Incremental system development | Mode                  |
| Maintenance                    | Mode                  |
| Normal operation               | Mode                  |
| Seasonal environmental change  | Scenario              |

Some conditions may legitimately be modeled in more than one way depending on the analytical purpose. The simulation designer should select the representation that best preserves the causal relationship being investigated.

---

## 6. Dynamic and Static Variables

Simulation design does not require every model variable to be dynamically simulated.

Depending on the purpose of a scenario or mode, the simulation may:

* hold primitive variables static;
* dynamically change primitive variables;
* calculate derived variables dynamically;
* directly prescribe certain derived values when appropriate.

For example:

```text
PRODUCTION_RATE =
    PRODUCER_EFFICIENCY
    * DOMAIN_TOTAL_DEMAND
    * ENVIRONMENT_EFFICACY
```

may normally be derived dynamically from primitive values.

However, a scenario may intentionally prescribe a particular production behavior if the purpose of the scenario is to test the system's response to that behavior rather than investigate its environmental cause.

The choice between primitive and derived dynamic variables is therefore a **simulation-design decision**.

When possible, primitive environmental and system parameters should be retained so that causal relationships remain visible.

---

## 7. System Performance Parameters

The principal system performance parameters currently defined for the Home Systems model are:

* **System Demand**

  * across resource domains,
  * across subsystems where applicable.

* **System Production**

  * across resource domains,
  * across subsystems.

* **Capital Cost**

These parameters provide the principal connection between simulation behavior and the subsequent analysis of system operational requirements.

The simulation should make it possible to observe how changes in these parameters affect operational outcomes across the defined scenario space.

---

## 8. Simulation Runs

A simulation run combines:

```text
Candidate System Concept
        +
Scenario
        +
Mode
        +
Model Parameters
        +
Simulation Time
        ↓
System Behavior
        ↓
Operational Outcomes
```

A run should be sufficiently defined that its results can be reproduced and interpreted.

The simulation designer should record the conditions necessary to answer:

* What scenario was evaluated?
* What mode was active?
* What candidate-system parameters were used?
* What environmental conditions were imposed?
* What time period was simulated?
* What operational outcomes occurred?
* What system state changes produced those outcomes?

---

## 9. Simulation Reporting

The simulation report is intended to translate raw simulation behavior into information useful for effectiveness analysis and operational-requirement derivation.

### 9.1 Primary Effectiveness Measure

The principal Home Systems effectiveness metric is **feasibility/self-sufficiency**.

The current formulation is:

$$
\frac{Capacity - OverheadLoss}{Demand} \cdot 100\%
$$

An inverse measure is used to represent **capital dependency**:

$$
\left(1 - \frac{Capacity - CapitalOverheadLoss}{Demand}\right) \cdot 100\%
$$

These measures may be applied:

* overall across domains and time
* per simulation tick
* per resource domain
* per tick per resource domain

The report should also provide ranges and duration-based measures where useful, such as:

* longest period of self-sufficiency
* longest period of dependency
* minimum feasibility
* maximum feasibility
* periods of sustained deficiency

The exact interpretation and boundary behavior of these metrics should be explicitly defined before they are used as validation criteria.

### 9.2 Contextual Reporting

Aggregate effectiveness alone is insufficient for interpreting a complex Home System.

The report should therefore preserve causal and contextual information that permits investigation of system behavior.

Examples include:

* which subsystem changed a state
* which resource was changed
* which transformation produced the change
* which formula was applied
* whether the transformation was accepted
* why a transformation was rejected
* what conditions existed when the transformation occurred
* which subsystem consumed or competed for a resource
* which resource became depleted
* which subsystem became a bottleneck
* when the system entered a degraded or failed condition

This allows simulation results to answer not only:

***Did the system succeed?***

but also:

***Why did the system succeed or fail?***

This distinction is important for deriving useful operational requirements.

---

## 10. Interpreting Simulation Results

Simulation results should be interpreted as evidence about the behavior and effectiveness of the candidate system concept under the defined operational conditions.

A failure does not automatically imply that the entire system concept is infeasible.

A failure may instead identify:

* a missing capability;
* an inadequate subsystem performance level;
* an environmental boundary;
* an insufficient resource reserve;
* a subsystem dependency;
* a competing resource demand;
* a bottleneck;
* or a requirement for an alternative operational mode.

Similarly, successful operation does not automatically establish that the candidate concept is adequate under all conditions. It establishes success only within the conditions represented by the relevant simulation runs.

The representative scenario space therefore matters as much as the individual results.

---

## 11. From Simulation Results to Operational Requirements

The purpose of the effectiveness analysis is ultimately to establish what the system must accomplish operationally.

Simulation results can reveal relationships such as:

```text
IF environmental condition X occurs,
THEN subsystem Y must provide capability Z
```

or:

```text
IF subsystem X produces capability Y,
THEN subsystem Z must provide capability A
```

These relationships can provide the basis for operational requirements.

However, a simulation result should not automatically be converted into a requirement in the same terms in which it appeared in the simulation.

The analytical process should distinguish between:

1. **Operational condition**
2. **Required operational outcome**
3. **System capability necessary to achieve the outcome**
4. **Performance level necessary to provide that capability**
5. **Physical implementation capable of providing that performance**

At the Needs Analysis level, the primary concern is the operational outcome and the functional capability required to achieve it.

For example, simulation analysis may reveal:

> During sufficiently low precipitation, the system becomes unable to maintain water availability unless additional stored water is available.

This can lead toward an operational requirement concerning maintaining adequate water availability during drought conditions.

Only subsequently should the analysis establish the required storage quantity, production capability, or physical implementation.

---

## 12. Example Requirement Derivation

Consider a drought scenario.

The simulation may vary:

```text
PRECIPITATION
WATER_PRODUCTION
STORAGE_CAPACITY
HOUSEHOLD_DEMAND
```

and observe:

```text
WATER_AVAILABILITY
```

The analysis may discover that below a particular storage level the system cannot maintain the required operational outcome for the duration of the drought.

The reasoning then becomes:

```text
Drought condition
        ↓
Reduced water production
        ↓
Storage is consumed
        ↓
Water availability falls below acceptable level
        ↓
Operational outcome is not achieved
```

Simulation can then determine the boundary at which the operational outcome becomes achievable:

```text
STORAGE_CAPACITY ≥ X
```

This provides evidence for a requirement concerning the necessary water-reserve capability.

The requirement should ultimately be expressed according to the appropriate level of abstraction rather than merely reproducing the simulation variable.

---

## 13. Design Principles for Scenario and Mode Crafters

Scenario and mode designers should follow these principles:

1. **Preserve causal separation.**
   External environmental conditions should generally be represented as scenarios, while conditions of the system itself should generally be represented as modes.

2. **Do not prescribe the outcome being evaluated.**
   A scenario should create the conditions to which the system responds rather than directly specifying whether the system succeeds or fails.

3. **Define normalized values semantically.**
   Every normalized quantity should have a meaningful relationship to the domain's independent normalization basis.

4. **Respect temporal meaning.**
   Rates, capacities, demands, and storage must have a consistent time basis.

5. **Prefer functional representation.**
   Do not introduce implementation-specific details when a functional abstraction is sufficient to evaluate system effectiveness.

6. **Preserve causal relationships.**
   Where possible, represent environmental and system parameters as primitive inputs and allow derived behavior to emerge through the model.

7. **Make scenarios reproducible.**
   Deterministic scenarios should produce repeatable results.

8. **Define the analytical purpose of each run.**
   Every scenario/mode combination should exist because it answers a question about system effectiveness.

9. **Capture context, not merely outcomes.**
   Results should make it possible to identify the cause of success, deficiency, or failure.

10. **Do not prematurely convert simulation variables into requirements.**
    Use simulation results to discover operational constraints and capabilities, then formulate requirements at the appropriate level of abstraction.

---

## 14. Overall Simulation Design

The simulation is therefore structured around four principal layers:

```text
┌───────────────────────────────────────────┐
│              ENVIRONMENT                  │
│                                           │
│  Scenarios                                │
│  Precipitation                            │
│  Geography                                │
│  External demand conditions               │
│  Other externally imposed conditions      │
└─────────────────────┬─────────────────────┘
                      │
                      ▼
┌───────────────────────────────────────────┐
│               SYSTEM                      │
│                                           │
│  Modes                                    │
│  Functional subsystems                    │
│  System parameters                        │
│  Resource transformations                 │
└─────────────────────┬─────────────────────┘
                      │
                      ▼
┌───────────────────────────────────────────┐
│              RESOURCE STATE               │
│                                           │
│  Capacity                                 │
│  Production                               │
│  Consumption                              │
│  Storage                                  │
│  Demand                                   │
│  Capital                                  │
└─────────────────────┬─────────────────────┘
                      │
                      ▼
┌───────────────────────────────────────────┐
│         OPERATIONAL OUTCOME               │
│                                           │
│  Feasibility                              │
│  Self-sufficiency                         │
│  Dependency                               │
│  Resource depletion                       │
│  Bottlenecks                              │
│  Failure modes                            │
│  Sustained operation                      │
└───────────────────────────────────────────┘
```

The simulation is ultimately an instrument for evaluating:

$$
\text{Candidate System}
+
\text{Operational Environment}
\rightarrow
\text{Operational Outcome}
$$

across a representative range of expected operational situations.

The resulting analysis provides the evidentiary basis for **Needs Validation** and for the subsequent formulation and refinement of **System Operational Requirements**.

---

[Back to Top](#home-systems-simulation-design)