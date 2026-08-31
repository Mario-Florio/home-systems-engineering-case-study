# Operational Effectiveness Analysis

- [Operational Effectiveness Analysis](#operational-effectiveness-analysis)
  - [Conceptual Model](#conceptual-model)
    - [System Performance Parameters](#system-performance-parameters)
      - [Resource Production Capacity](#resource-production-capacity)
      - [Inhabitant Resource Demand](#inhabitant-resource-demand)
      - [Overhead Cost](#overhead-cost)
    - [Measures of Effectiveness](#measures-of-effectiveness)
      - [Feasibility (Self-Sufficiency)](#feasibility-self-sufficiency)
      - [Capital Dependency](#capital-dependency)
    - [Operational Modes](#operational-modes)
    - [Operational Scenarios](#operational-scenarios)
  - [Simulation](#simulation)

---

## Conceptual Model

### System Performance Parameters

#### Resource Production Capacity

The amount of resources produced by the home system.

**Domains:**

* Food
* Water
* Electricity
* Shelter
* Conditioned Climate
* Information

---

#### Inhabitant Resource Demand

The required support by inhabitants.

**Domains:**

* Food
* Water
* Electricity
* Shelter
* Conditioned Climate
* Information

---

#### Overhead Cost

The amount of required overhead to maintain system operation.

* Capital
* Labor

---

### Measures of Effectiveness

#### Feasibility (Self-Sufficiency)

The degree to which a system can satisfy required demand under its available capacity constraints. Measures the percentage of demand that can be satisfied by available capacity.

$$
\frac{Capacity - OverheadLoss}{Demand} \cdot 100\%
$$

* *Capacity* — Any total resource production amount (domain-scoped, or system-wide)
* *OverheadLoss* — The amount of total overhead loss (including *capital*, *labor*, etc.) per capacity
* *Demand* — The amount of *demand* associated with resource capacity in question

---

#### Capital Dependency

The degree to which a system depends on external capital to maintain operational capacity. Measures the percentage of capital demand to produce capacity.

$$
\left(1 - \frac{Capacity - CapitalOverheadLoss}{Demand}\right) \cdot 100\%
$$

* *Capacity* — Any total resource production amount (domain-scoped, or system-wide)
* *CapitalOverheadLoss* — The amount of capital overhead loss per capacity (does not include *labor* or other non-capital overhead costs)
* *Demand* — The amount of *demand* associated with resource capacity in question

---

### Operational Modes

* Normal
* Installation
* Maintenance
* Storage
* Transportation

> Disclaimer: At current level of development, certain operational modes, such as installation and transport, may not be warranted until further implementation details are materialized.

---

### Operational Scenarios

* Average weather year
* Average infrastruture degradation
* Summer drought
* Winter power outage
* etc.

---

## Simulation

TBD.

---
