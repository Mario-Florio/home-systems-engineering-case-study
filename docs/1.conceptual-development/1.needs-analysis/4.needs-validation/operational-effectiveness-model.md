# Operational Effectiveness Model

**Contents:**

- [1. Purpose](#1-purpose)
- [2. Model Architecture](#2-model-architecture)
- [3. System Representation](#3-system-representation)
  - [3.1 System-Level Abstraction](#31-system-level-abstraction)
  - [3.2 Subystem Functions](#32-subsystem-functions)
  - [3.3 Functional Elements](#33-functional-elements)
  - [3.4 Resources](#34-resources)
- [4. Environment](#4-environment)
- [5. Performance Parameters](#5-performance-parameters)
  - [5.1 Resource Production and Consumption](#51-resource-production-and-consumption)
  - [5.2 Primitive Performance Parameters](#52-primitive-performance-parameters)
- [6. Resource Domains](#6-resource-domains)
  - [6.1 Food](#61-food)
  - [6.2 Water](#62-water)
  - [6.3 Electricity](#63-electricity)
  - [6.4 Conditioned Environment](#64-conditioned-environment)
  - [6.5 Capital](#65-capital)
- [7. Parameter Derivation](#7-parameter-derivation)
- [8. System State](#8-system-state)
- [9. Transformations](#9-transformations)
- [10. Operational Modes](#10-operational-modes)
- [11. Scenarios](#11-scenarios)
- [12. Measures of Effectiveness](#12-measures-of-effectiveness)
- [13. Operational Effectiveness Analysis](#13-operational-effectiveness-analysis)
- [14. Model Abstraction and Scope](#14-model-abstraction-and-scope)
  - [14.1 Functional rather than physical representation](#141-functional-rather-than-physical-representation)
  - [14.2 Performance rather than mechanism](#142-performance-rather-than-mechanism)
  - [14.3 Resource-domain separation](#143-resource-domain-separation)
  - [14.4 Explicit environment](#144-explicit-environment)
  - [14.5 State/parameter separation](#145-stateparameter-separation)
  - [14.6 Extensible transformations](#146-extensible-transformations)
  - [14.7 Derived effectiveness](#147-derived-effectiveness)
- [15. Model Extensibility](#15-model-extensibility)
- [16. Summary](#16-summary)

---

## 1. Purpose

The Operational Effectiveness Model (OEM) is the system-level model used as the object of study in the Operational Effectiveness Analysis (OEA). It provides a formal representation of a candidate system concept sufficient to simulate its operation under a defined set of environmental conditions, operational modes, and scenarios, and subsequently evaluate its operational effectiveness.

The OEM is intended for use at the level of abstraction appropriate to the **Needs Analysis** stage of the Systems Engineering lifecycle. Accordingly, the model describes the system principally in terms of its functional elements, resources, performance characteristics, environmental relationships, and operational behavior. It does not attempt to represent the detailed physical implementation or internal mechanisms of the system unless those mechanisms materially influence system-level operational behavior.

The model is therefore principally **declarative in its representation of system performance**. A functional element is characterized by the performance it provides rather than by an imperative simulation of the physical processes through which that performance would be achieved.

For example, a candidate home system may contain a *Produce Food* functional element representing an agricultural system. The OEM need not model photosynthesis, crop growth, soil chemistry, harvesting, or other agricultural mechanisms. Instead, the functional element may be declared to possess a particular production capacity, efficiency, resource demand, and environmental sensitivity. These declared characteristics are subsequently used by the model's transformations to determine operational behavior.

The OEM consequently establishes a boundary between **what the system is capable of doing** and **how the system achieves that capability**. The former is represented by the OEM; the latter is principally a concern of subsequent system definition and design.

---

## 2. Model Architecture

The OEM is organized into several conceptual components:

1. **System**
2. **Environment**
3. **Performance Parameters**
4. **Transformations**
5. **Operational Modes**
6. **Scenarios**
7. **Measures of Effectiveness**

Not every component must necessarily be represented with the same degree of detail in every application. In particular, some subsystem functions, resources, parameters, or transformations may be omitted where they do not materially influence system-level operational behavior.

At a high level:

```text
Operational Effectiveness Model
│
├── System
│   ├── Subsystem Functions
│   └── Functional Elements / Resources
│
├── Environment
│   ├── Environmental Elements
│   └── Environmental Conditions
│
├── Performance Parameters
│   ├── Production
│   ├── Consumption / Demand
│   ├── Storage / Capacity
│   ├── Efficiency
│   └── Environmental Efficacy
│
├── Transformations
│   └── System State Transitions
│
├── Modes
│   ├── Operational
│   └── Non-operational
│       ├── Transportation
│       └── Development
│
├── Scenarios
│   └── Environmental Conditions
│
└── Measures of Effectiveness
    └── Derived Operational Outcomes
```

These components should be understood as complementary rather than independent. Performance parameters describe characteristics of the system; the environment provides conditions under which those characteristics are realized; transformations determine how the system changes as it operates; modes and scenarios establish the circumstances under which those transformations occur; and Measures of Effectiveness evaluate the resulting operational behavior.

---

## 3. System Representation

### 3.1 System-Level Abstraction

The system is represented at the level of its **subsystem functions, functional elements, and their relationships**.

At the Needs Analysis level, system decomposition remains principally functional and conceptual rather than physical. The model therefore identifies the functions that the system performs and the domain-agnostic functional elements that are produced, consumed, stored, transmitted, or otherwise acted upon by those functions.

This distinction is important. A function describes **what the system does**, whereas a functional element describes **what is acted upon, transmitted, or transformed by the system**.

For example:

*`ProduceFood(Capital, Labor, Resources) → Food`*

`ProduceFood` is a system function. `Food` is a functional element.

The OEM does not necessarily prescribe the physical implementation through which a function is performed. A *Produce Food* function may be implemented through outdoor agriculture, a greenhouse, domestic livestock, wildlife hunting or another implementation while retaining the same system-level functional representation.

---

### 3.2 Subsystem Functions

The current Home Systems model identifies the following principal subsystem functions, derived from the [Functional Analysis](../2.functional-analysis/functional-analysis.md):

* Produce Food
* Produce Water
* Generate Electricity
* Provide Shelter
* Control Climate
* Store Resource
* Communication Connection
* Waste Management

These functions describe the principal activities performed by the Home System. These subsystem functions operate upon functional elements and establish transformations between them.

For example:

```text
Produce Food
    ├── consumes Capital
    ├── consumes Labor
    ├── consumes Water
    ├── consumes Electricity
    └── produces Food
```

The function establishes the operational relationship; the resources involved are the functional elements participating in that relationship.

Not all functions necessarily require explicit representation in every OEM. A function should be represented where its behavior materially influences system-level operational behavior or a Measure of Effectiveness.

The list of functions is therefore extensible and should not be regarded as a closed abstraction.

---

### 3.3 Functional Elements

Functional elements are the low-level, domain-agnostic elements that are transmitted throughout, consumed by, produced by, stored within, or otherwise acted upon by the system.

In general systems engineering terms, functional elements may be categorized into domains such as:

* Material
* Energy
* Information

Information may be further distinguished, where useful to the analysis, into:

* Data
* Signals

The Home Systems Model uses the concept of **Resources** to represent these functional elements at the system level.

The current resource representation is:

| Resource                | Functional Element |
| ----------------------- | ------------------ |
| Capital                 | Material, Signal   |
| Labor                   | Material, Energy   |
| Resources               | TBD                |
| Food                    | Material, Energy   |
| Water                   | Material, Energy   |
| Electricity             | Energy             |
| Shelter                 | Material           |
| Conditioned Environment | Energy             |
| Information             | Data, Signal       |

> For further elaboration on resource definitions, see the [Functional Elements](../2.functional-analysis/functional-analysis.md#functional-elements) section of the *Functional Analysis*.

The classification is not necessarily intended to provide a complete physical ontology of each resource. Rather, it identifies the functional-element domains through which each resource participates in system operation.

For example, Food is principally a Material functional element, but may also represent embodied Energy for purposes of the system model. Electricity is an Energy functional element. Information is represented principally as Data and Signal.

`Resources` is retained as an abstraction for resources not yet explicitly established by the model. All such elements are, by definition, Resources within the Home Systems Model.

---

### 3.4 Resources

Resources are therefore the Home Systems Model's representation of **functional elements**.

A resource represents a quantity that may be produced, consumed, stored, transferred, acquired, or otherwise transformed by the system.

The current resource domains are:

* Capital
* Labor
* Food
* Water
* Electricity
* Shelter
* Conditioned Environment
* Information

The `Resources` abstraction may additionally represent resources that have not yet been explicitly incorporated into the model.

Resources are represented as distinct domains because quantities belonging to different resource domains are not generally interchangeable for purposes of system-state evaluation.

For example:

$$
Food = Food_{Production} - Food_{Consumption}
$$

is a valid resource-domain operation, whereas:

$$
Food = Water_{Production} - Food_{Consumption}
$$

is not.

The resource domain therefore establishes a fundamental constraint on valid transformations and evaluations.

A resource should consequently be understood not merely as a scalar quantity, but as a typed functional element belonging to a particular resource domain.

---

## 4. Environment

The system environment is an explicit component of the OEM.

The environment represents external conditions that affect system performance but are not themselves system resources or functions.

The current Home Systems model identifies three principal environmental domains:

* Climate
* Geography
* Economy

These environmental elements may be represented as heterogeneous objects rather than as a single homogeneous environmental state.

The environment interacts with system functions and functional elements through the model's transformations.

For example, climate and geography may affect the efficacy of the *Produce Food* function, while the economy may establish the cost associated with externally acquiring a resource or maintaining, improving, or repairing existing subsystems.

The environment also establishes the conditions under which **scenarios** are evaluated. A scenario represents a postulated action or encounter to which the system must respond.

---

## 5. Performance Parameters

Performance Parameters describe the characteristics of the system's functions and functional elements that determine operational capability.

They are the principal declared inputs to the operational model.

The current Home Systems model organizes these parameters primarily around:

1. Resource Production Capacity
2. Resource Consumption Rate
3. Overhead Cost

These parameters describe the performance of system functions with respect to particular functional elements.

For example:

```text
Produce Food
    → Food Production Rate
    → Water Demand
    → Electricity Demand
```

The function is therefore the source of the operational relationship, while the resource domain identifies the functional element upon which that relationship operates.

Production and consumption rates are generally not primitive parameters. They are derived from lower-level performance characteristics such as function efficiency, environmental efficacy, resource availability, and other applicable conditions.

---

### 5.1 Resource Production and Consumption

For the current Home Systems model, the principal system-level production and consumption parameters are:

* Food Production Rate
* Food Consumption Rate
* Water Production Rate
* Water Consumption Rate
* Electricity Production Rate
* Electricity Consumption Rate
* Conditioned Climate Production Rate
* Conditioned Climate Consumption Rate

These rates describe flows of functional elements resulting from the operation of system functions.

For example:

```text
Produce Food
    → produces Food
```

results in a Food Production Rate, while:

```text
Produce Food
    → consumes Water
```

results in a Water demand attributable to the *Produce Food* function.

---

### 5.2 Primitive Performance Parameters

The lower-level parameters from which production and consumption behavior is derived generally consist of:

* Storage
* Maximum Storage
* Subsystem Demand
* Prinicipal Subsystem Producer Efficiency
* Environmental Performance Multipliers

These parameters describe the characteristics of the system and its functions without prescribing the detailed physical mechanisms through which those characteristics are realized.

For example:

```text
ClimateEfficacy       = 1
GeographyEfficacy     = 1
ProduceFoodEfficiency = 1
TotalSystemFoodDemand = 7

FoodProductionRate =
    ClimateEfficacy
    * GeographyEfficacy
    * ProduceFoodEfficiency
    * TotalSystemFoodDemand
```

Here, `ProduceFoodEfficiency` is a performance parameter of the *Produce Food* function, while `FoodProductionRate` is a resulting flow of the Food functional element.

---

## 6. Resource Domains

Resource domains organize the functional elements that participate in the Home Systems Model's resource-capacity dynamics.

Each domain contains the parameters and state variables relevant to that resource.

The domain structure is therefore not a decomposition of system functions. It is a decomposition of the **functional elements exchanged between functions**.

For example:

```text
Produce Food ────────► Food
     │
     ├───────────────► Water
     │
     └───────────────► Electricity
```

The *Produce Food* function crosses multiple resource domains because it operates upon multiple functional elements.

---

### 6.1 Food

The current Food domain contains:

* Storage `[0,∞)`
* Maximum Storage `[0,∞)`
* Inhabitant Demand `[0,∞)`
* Produce-Food Demand `[0,∞)`
* Produce-Food Efficiency `[0,1]`
* Climate Efficacy `[0,1]`
* Geography Efficacy `[0,1]`

Storage represents the quantity of the Food functional element presently held by the system.

Maximum Storage establishes the system's capacity to retain Food.

Inhabitant Demand represents direct consumption of Food by system inhabitants.

Produce-Food Demand represents Food consumed by the *Produce Food* function where Food itself is an operational input.

Produce-Food Efficiency represents the performance of the *Produce Food* function with respect to producing the Food functional element.

Climate and Geography Efficacy represent environmental performance multipliers affecting that function.

---

### 6.2 Water

The current Water domain contains:

* Storage `[0,∞)`
* Maximum Storage `[0,∞)`
* Inhabitant Demand `[0,∞)`
* Produce-Food Demand `[0,∞)`
* Control-Climate Demand `[0,∞)`
* Store-Food Demand `[0,∞)`
* Produce-Water Efficiency `[0,1]`
* Climate Efficacy `[0,1]`
* Geography Efficacy `[0,1]`

Water demonstrates the distinction between functions and functional elements particularly clearly.

`Produce-Food Demand` is not itself a function or subsystem. It is a demand for the Water functional element generated by the *Produce Food* function.

Thus:

```text
Produce Food
    └── Water Demand
             ↓
          Water
```

The demand is represented within the Water domain because Water is the functional element being consumed.

---

### 6.3 Electricity

The current Electricity domain contains:

* Storage
* Maximum Storage
* Inhabitant Demand
* Produce-Food Demand
* Produce-Water Demand
* Control-Climate Demand
* Store-Food Demand
* Store-Water Demand
* Generate-Electricity Efficiency
* Climate Efficacy
* Geography Efficacy

As with Water, the demands identify functions that consume the Electricity functional element.

For example:

```text
Produce Food
    └── Electricity Demand
             ↓
        Electricity
```

while:

```text
Generate Electricity
    └── Electricity Production
                 ↓
            Electricity
```

The Electricity domain therefore represents the functional element and its state, while the functions establish the production and consumption relationships.

---

### 6.4 Conditioned Environment

The Conditioned Environment domain represents a functional element corresponding principally to the energy associated with maintaining an internal environmental condition.

It contains:

* Storage
* Maximum Storage
* Inhabitant Demand
* Produce-Food Demand
* Store-Food Demand
* Store-Electricity Demand
* Control-Climate Efficiency
* Climate Efficacy
* Geography Efficacy

The domain is somewhat more abstract than Food, Water, or Electricity.

Storage may represent characteristics such as insulation or thermal retention. Demand may represent the energy required to maintain the desired internal condition.

The domain is therefore optional and should primarily be included where conditioned-environment behavior materially affects the operational analysis (e.g., modeling the rate at which shelter or storage dissipates temperate air).

---

### 6.5 Capital

Capital is a functional element with a somewhat different role from the physical resource domains. It principally represents material and signal flows associated with economic resources and financial dependency.

The current Capital domain contains:

* Storage
* Inhabitant Demand
* Produce-Food Demand
* Produce-Water Demand
* Generate-Electricity Demand
* Control-Climate Demand
* Store-Food Demand
* Store-Water Demand
* Store-Electricity Demand
* Inhabitant Income `[0,1]`
* Economy Food Cost `[0,∞)`
* Economy Water Cost `[0,∞)`
* Economy Electricity Cost `[0,∞)`
* Economy Waste-Removal Cost `[0,∞)`

Capital Demand represents the Capital functional element consumed by the operation of functions.

Economy Costs may therefore serve as consumption-rate primitives when a function fails to satisfy an internal resource demand and the system acquires the required functional element externally.

For example:

```text
Produce Food < Food Demand
        ↓
External Food Acquisition
        ↓
Capital Consumption
```

Economy Costs may also serve as production-rate primitives where the model permits the sale of surplus resources.

The distinction between acquisition cost and sale price may subsequently warrant separate parameters if required by the operational model.

---

## 7. Parameter Derivation

Performance parameters should be distinguished from the quantities produced by the operational simulation.

For example:

```text
Produce-Food Efficiency
Climate Efficacy
Geography Efficacy
```

are declared characteristics.

By contrast:

```text
Food Production Rate
Food Storage
Food Consumption
```

may be operational quantities derived from those characteristics.

A simplified relationship is:

$$
P_r =
\eta_s
\times
E_e
\times
E_f
\times
D_r
$$

where:

- $P_r$ = production rate for resource $r$
- $\eta_s$ = subsystem producer efficiency
- $E_e$ = environmental efficacy
- $E_f$ = other applicable performance factors
- $D_r$ = relevant system demand or production basis

The precise formulation of these relationships belongs to the **Transformations** portion of the OEM and is therefore intentionally not fixed by this section.

---

## 8. System State

The operational model maintains a system state representing the quantities relevant to operational behavior at a given point in time.

At minimum, the state may contain the current values of resource quantities such as:

```text
Food Storage
Water Storage
Electricity Storage
Conditioned Environment Storage
Capital Storage
```

State is distinguished from Performance Parameters.

A Performance Parameter describes a characteristic of the system:

```text
ProduceFoodEfficiency = 0.8
```

while State describes the current operational condition:

```text
FoodStorage = 4.2
```

The distinction is important because parameters generally remain fixed for a particular system instantiation, while state changes as the system operates.

The simulation may consequently be understood as evaluating:

$$
S_{t+1} = T(S_t,P,E_t,M_t)
$$

where:

* $S_t$ = the system state at time \(t\)
* $P$ = the set of system performance parameters
* $E_t$ = the environmental state
* $M_t$ = the current operational mode
* $T$ = the applicable set of transformations

The resulting state $S_{t+1}$ becomes the input to the next operational step.

---

## 9. Transformations

Transformations define the operational dynamics of the OEM.

Where Performance Parameters describe **what the system possesses**, Transformations describe **how those characteristics produce changes in system state**.

A transformation may:

* produce a resource;
* consume a resource;
* transfer a resource;
* modify storage;
* impose a demand upon another functional element;
* respond to an environmental condition;
* respond to a system state condition;
* trigger a fallback or external dependency;
* modify another system parameter or state value; or
* otherwise establish a relationship between elements of the operational model.

For example:

```text
Produce Food
    ├── requires Water
    └── produces Food
```

may be represented by a transformation in which food production occurs only when sufficient water is available:

```text
FoodProduction =
    ProduceFoodPerformance
    if WaterStorage >= ProduceFoodWaterDemand
    otherwise 0
```

and the corresponding state transition may be represented conceptually as:

```text
Water -= ProduceFoodWaterDemand
Food  += FoodProductionRate
```

The complete set of transformations is intentionally left extensible. Their formal specification constitutes a subsequent portion of the OEM.

Transformations should remain at the same level of abstraction as the rest of the model. They should describe operational relationships rather than introduce unnecessary implementation-level mechanisms.

---

## 10. Operational Modes

An operational mode represents a deterministic behavioral condition of the system.

Modes may describe both operational and non-operational conditions, including, for example:

* Normal Operation
* Development
* Transportation
* Maintenance
* Storage
* Failure
* Recovery

The precise set of modes is system-dependent.

Modes differ from scenarios in that a mode principally describes **internal system behavior**, while a scenario describes a **postulated encounter between the system and its environment**.

A mode may therefore modify which transformations are active, their performance, or the resources they consume.

For example:

```text
Normal Operation
    → normal production and consumption

Transportation
    → production disabled
    → transportation consumption enabled

Maintenance
    → production reduced or disabled
    → maintenance demand enabled
```

Mode behavior is represented by the OEM and subsequently exercised by the simulation.

---

## 11. Scenarios

A scenario represents a postulated action or environmental condition to which the system must respond.

Scenarios provide the operational context in which the system is evaluated.

A scenario may specify:

* environmental conditions;
* external events;
* resource availability;
* demands placed upon the system;
* changes in environmental performance;
* system interactions;
* operational duration;
* or other conditions relevant to system effectiveness.

The distinction between scenario and mode should be preserved:

```text
Scenario = what the system encounters

Mode = how the system internally operates under that condition
```

A scenario may therefore cause a transition between modes without itself being a mode.

Scenarios should be capable of representing both expected and adverse operational conditions where those conditions are relevant to the needs being analyzed.

---

## 12. Measures of Effectiveness

Measures of Effectiveness (MoEs) provide the principal means by which simulated operational behavior is evaluated.

An MoE is not itself a system parameter. It is a derived evaluation of the system's performance relative to an operational objective.

Conceptually:

$$
MoE = f(S_0,S_1,\ldots,S_n,E,M)
$$

where the MoE is derived from one or more states over the operational period and, where appropriate, the scenarios and modes under which those states occurred.

The Home Systems model currently anticipates Measures of Effectiveness relating to concepts such as:

* Self-Sufficiency
* Capital Dependency

These are not necessarily primitive quantities within the OEM. They are derived from the operational behavior of the system.

The formal definition of individual MoEs, including their normalization, aggregation, thresholds, and interpretation, is intentionally deferred to the MoE specification.

This allows additional effectiveness measures to be introduced without changing the underlying system representation.

---

## 13. Operational Effectiveness Analysis

The OEM provides the model; the simulation provides an execution of that model; OEA evaluates the resulting operational behavior.

The relationship may therefore be represented as:

```text
System Concept
      │
      ▼
Operational Effectiveness Model
      │
      ├── System
      ├── Environment
      ├── Performance Parameters
      ├── Transformations
      ├── Operational Modes
      └── Scenarios
      │
      ▼
Simulation
      │
      ▼
Operational Behavior
      │
      ▼
Measures of Effectiveness
      │
      ▼
Operational Effectiveness Analysis
```

The simulation should consequently not be understood as the model itself.

The OEM specifies the system-level operational concept. The simulation executes that concept across time and under specified conditions. The resulting operational history provides the evidence from which effectiveness is evaluated.

---

## 14. Model Abstraction and Scope

The OEM is deliberately constrained to the level of abstraction appropriate to system-level Needs Analysis.

It should therefore avoid modeling implementation details unless those details materially alter system-level performance.

This produces several important modeling principles.

### 14.1 Functional rather than physical representation

Functional elements describe capabilities rather than physical implementations.

### 14.2 Performance rather than mechanism

The model declares performance characteristics rather than reproducing the physical mechanisms responsible for those characteristics.

### 14.3 Resource-domain separation

Resources remain distinct domains unless an explicit transformation establishes a relationship between them.

### 14.4 Explicit environment

Environmental conditions are modeled explicitly rather than being implicitly embedded within system parameters.

### 14.5 State/parameter separation

Declared system characteristics are distinguished from operational state.

### 14.6 Extensible transformations

System behavior is defined through explicit transformations rather than being embedded within individual parameter definitions.

### 14.7 Derived effectiveness

Measures of Effectiveness are derived from operational behavior rather than being treated as direct system inputs.

---

## 15. Model Extensibility

The OEM is intended to provide a stable framework into which additional system-level concepts can be introduced.

The principal extension points are:

```text
System
    → additional resources
    → additional subsystems

Environment
    → additional environmental domains
    → additional environmental conditions

Performance Parameters
    → additional performance characteristics
    → additional resource-domain parameters

Transformations
    → additional resource flows
    → conditional relationships
    → failure and recovery behavior
    → state transitions

Operational Modes
    → additional operational and non-operational conditions

Scenarios
    → additional postulated encounters

Measures of Effectiveness
    → additional operational objectives
    → additional derived metrics
```

Extensions should be introduced only where they contribute materially to the level of analysis being performed. The objective is not to produce a complete physical simulation of the system, but a sufficient operational representation from which meaningful effectiveness judgments can be derived.

---

## 16. Summary

The Operational Effectiveness Model represents a candidate system concept as a declarative, system-level model of operational capability.

Its principal elements are:

$$
\boxed{
OEM =
System +
Environment +
Parameters +
Transformations +
Modes +
Scenarios +
MoEs
}
$$

The **System** establishes what functional elements and resources exist.

The **Environment** establishes the external conditions under which the system operates.

**Performance Parameters** declare the characteristics and capabilities possessed by the system.

**Transformations** define how those characteristics interact to produce changes in system state.

**Operational Modes** define deterministic internal behavioral conditions.

**Scenarios** define the postulated encounters and environmental conditions against which the system is exercised.

**Measures of Effectiveness** evaluate the resulting operational behavior relative to the objectives of the analysis.

The resulting model is intentionally declarative and system-level. It describes the performance characteristics of a candidate concept without requiring the detailed implementation mechanisms through which those characteristics are achieved. This permits the OEM to serve as a common operational representation for different candidate implementations while retaining sufficient structure to simulate resource dynamics, environmental interactions, operational modes, scenarios, and resulting effectiveness.

---

[Back to Top](#operational-effectiveness-model)