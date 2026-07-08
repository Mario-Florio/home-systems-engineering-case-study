# Feasibility Definition

- [Feasibility Definition](#feasibility-definition)
  - [1. Feasibility Criteria](#1-feasibility-criteria)
    - [Technical](#technical)
    - [Environment](#environment)
    - [Stakeholder](#stakeholder)
  - [2. Candidate Subsystem Technologies](#2-candidate-subsystem-technologies)
    - [Candidate Concept](#candidate-concept)
  - [3. Compatibility Assessment](#3-compatibility-assessment)
    - [Technical Compatibility](#technical-compatibility)
      - [Food](#food)
      - [Water](#water)
      - [Electricity](#electricity)
      - [Shelter](#shelter)
      - [Conditioned Environment](#conditioned-environment)
      - [Information](#information)
      - [Waste Management](#waste-management)
      - [Shared Dependencies](#shared-dependencies)
      - [Result](#result)
    - [Environment Compatibility](#environment-compatibility)
      - [Climate](#climate)
      - [Geography](#geography)
      - [Economy](#economy)
      - [Shared Dependencies](#shared-dependencies-1)
      - [Result](#result-1)
    - [Stakeholder Compatibility](#stakeholder-compatibility)
      - [Affordability](#affordability)
      - [Operational Coverage](#operational-coverage)
      - [Labor](#labor)
      - [Result](#result-2)
    - [Compatibility Results](#compatibility-results)
  - [4. Development Considerations](#4-development-considerations)
    - [Development Strategy](#development-strategy)
      - [Architectural Principles](#architectural-principles)
      - [Economic Priorities](#economic-priorities)
    - [Production Considerations](#production-considerations)
      - [Availability of Materials](#availability-of-materials)
      - [Availability of Contractors](#availability-of-contractors)
      - [Regulatory Concerns](#regulatory-concerns)
      - [Construction Sequencing](#construction-sequencing)
    - [Risks](#risks)
      - [Shared Dependencies](#shared-dependencies-2)
        - [Electricity](#electricity-1)
        - [Solar Radiation](#solar-radiation)
        - [Precipitation](#precipitation)
        - [Land Area](#land-area)
      - [Verdict](#verdict)
  - [5. Concept of Operations](#5-concept-of-operations)
    - [Normal Operation](#normal-operation)
      - [Food](#food-1)
      - [Water](#water-1)
      - [Electricity](#electricity-2)
    - [Seasonal Operation](#seasonal-operation)
      - [Spring](#spring)
      - [Summer](#summer)
      - [Autumn](#autumn)
      - [Winter](#winter)
    - [Human Participation](#human-participation)
      - [Daily](#daily)
      - [Weekly](#weekly)
      - [Seasonal](#seasonal)
      - [Abnormal](#abnormal)
    - [Maintenance Concept](#maintenance-concept)
      - [Routine](#routine)
      - [Preventive](#preventive)
      - [Corrective](#corrective)
      - [Long-Term](#long-term)
    - [Abnormal Operation](#abnormal-operation)
      - [Power Outage](#power-outage)
      - [Drought](#drought)
      - [Operator Illness](#operator-illness)
  - [6. Evaluation Strategy](#6-evaluation-strategy)
  - [7. Feasible System Concept](#7-feasible-system-concept)

---

## 1. Feasibility Criteria

### Technical

* All subsystem functions possess at least one plausible realization.
* The resulting subsystem technologies are technically compatible.
* Necessary system interfaces are realizable.

### Environment

* The concept is compatible with environmental conditions.
* Required natural resources are reasonably available.

### Stakeholder

* Capital investment is within acceptable limits.
* Operational cost satisfies operational objectives.
* Labor requirements are compatible with stakeholder lifestyle.
* Concept supports desired concept of operations.

---

## 2. Candidate Subsystem Technologies

| Function                 | Candidate Technologies                        |
| ------------------------ | --------------------------------------------- |
| Produce Food             | Agriculture, External Purchase                |
| Produce Water            | Precipitation Capture, Well, Municipal Supply |
| Generate Electricity     | Solar, Utility Grid                           |
| Provide Shelter          | House, Garage, Workshop                       |
| Control Climate          | HVAC, Refrigeration                           |
| Communication Connection | Internet, Phone Service                       |
| Waste Management         | Plumbing, Recycling, Municipal Service        |

### Candidate Concept

```text
Produce Food → Food
    Agriculture
    External Purchase (backup)

Produce Water → Water
    Precipitation Capture (primary source)
    Well
    Municipal Supply (backup)

Generate Electricity → Electricity
    Solar
    Utility Grid (backup)

Provide Shelter → Shelter
    House
    Garage
    Workshop

Control Climate → Conditioned Environment
    HVAC
    Refrigeration

Communication Connection → Information
    Internet
    Phone Service

Waste Management
    Plumbing
    Recycling
    Municipal Service
```

---

## 3. Compatibility Assessment

### Technical Compatibility

#### Food

| Implementation    | Dependency      | Supporting Implementation(s)                   |
| ----------------- | --------------- | ---------------------------------------------- |
| Agriculture       | Water           | Precipitation Caputure, Well, Municipal Supply |
| Agriculture       | Electricity     | Solar, Utility Grid                            |
| External Purchase | -               | -                                              |

**Flows:**

*Precipitation Capture* ∨ *Well* ∨ *Municipal Supply* : **Water** → *Agriculture*

*Solar* ∨ *Utility Grid* : **Electricity** → *Agriculture*

**Functional Model:**

*`Agriculture(PrecipitationCaputure() or Well() or MunicipalSupply(), Solar() or UtilityGrid()) → Food`*

---

#### Water

| Implementation        | Dependency  | Supporting Implementation(s) |
| --------------------- | ----------- | ---------------------------- |
| Precipitation Capture | Electricity | Solar, Utility Grid          |
| Well                  | Electricity | Solar, Utility Grid          |
| Municipal Supply      | -           | -                            |

**Flows:**

*Solar* ∨ *Utility Grid* : **Electricity** → *Precipitation Capture* ∧ *Well*

**Functional Model:**

*`PrecipitationCaputure(Solar() or UtilityGrid()) → Water`*

*`Well(Solar() or UtilityGrid()) → Water`*

---

#### Electricity

| Implementation | Dependency | Supporting Implementation(s) |
| -------------- | ---------- | ---------------------------- |
| Solar          | -          | -                            |
| Utility Grid   | -          | -                            |

---

#### Shelter

| Implementation | Dependency | Supporting Implementation(s) |
| -------------- | ---------- | ---------------------------- |
| House          | -          | -                            |
| Garage         | -          | -                            |
| Workshop       | -          | -                            |

---

#### Conditioned Environment

| Implementation   | Dependency  | Supporting Implementation(s) |
| ---------------- | ----------- | ---------------------------- |
| HVAC             | Electricity | Solar, Utility Grid          |
| Refrigeration    | Electricity | Solar, Utility Grid          |

**Flows:**

*Solar* ∨ *Utility Grid* : **Electricity** → *HVAC* ∧ *Refrigeration*

**Functional Model:**

*`HVAC(Solar() or UtilityGrid()) → Conditioned Environement`*

*`Refrigeration(Solar() or UtilityGrid()) → Conditioned Environment`*

---

#### Information

| Implementation | Dependency  | Supporting Implementation(s) |
| -------------- | ----------- | ---------------------------- |
| Internet       | Electricity | Solar, Utility Grid          |
| Phone Service  | Electricity | Solar, Utility Grid          |

**Flows:**

*Solar* ∨ *Utility Grid* : **Electricity** → *Internet* ∧ *Phone Service*

**Functional Model:**

*`Internet(Solar() or UtilityGrid()) → Information`*

*`PhoneService(Solar() or UtilityGrid()) → Information`*

---

#### Waste Management

| Implementation    | Dependency | Supporting Implementation(s)                  |
| ----------------- | ---------- | --------------------------------------------- |
| Plumbing          | Water      | Precipitation Capture, Well, Municipal Supply |
| Recycling         | -          | -                                             |
| Municipal Service | -          | -                                             |

**Flows:**

*Precipitation Capture* ∧ *Well* ∧ *Municipal Supply* : **Water** → *Plumbing*

**Functional Model:**

*`Plumbing(PrecipitationCapture() or Well() or MunicipalSupply())`*

---

#### Shared Dependencies

| Dependency    | Dependent Technologies                                          | Resource Domain(s)                            |
| ------------- | --------------------------------------------------------------- | --------------------------------------------- |
| Electricity   | Agriculture, Well, HVAC, Refrigeration, Internet, Phone Service | Food, Water, Conditioned Climate, Information |
| Water         | Agriculture, Waste Management                                   | Food, Water                                   |

---

#### Result

* **System is technologically coherent at subsystem level**
* All subsystem candidate technology dependencies can be supported by peer subsystems
* **Risk** — Electricity represents a critical shared dependency whose failure propagates across multiple subsystems

---

### Environment Compatibility

System environment is undetermined, thus compatibility will be determined in terms of conditional needs (e.g., concept is feasible **if** condition *x* is met).

> **Disclaimer:** Resource dependency is demonstrative rather than conclusive.

---

#### Climate

| Function             | Implementation        | Dependency                                                                                              |
| -------------------- | --------------------- | ------------------------------------------------------------------------------------------------------- |
| Produce Food         | Agriculture           | Precipitation, Temperature, Humidity / Aridity, Solar Radiation, Growing Season Length, Frost Frequency |
| Produce Water        | Precipitation Capture | Precipitation                                                                                           |
| Produce Water        | Well                  | Precipitation, Humidity / Aridity                                                                       |
| Generate Electricity | Solar                 | Solar Radiation                                                                                         |

> **Note:** Multiple subsystem technologies depend on climates *precipitation*

---

#### Geography

| Function             | Implementation        | Dependency                            |
| -------------------- | --------------------- | ------------------------------------- |
| Produce Food         | Agriculture           | Land Area, Soil Viability, Topography |
| Produce Water        | Precipitation Capture | Land Area                             |
| Produce Water        | Well                  | Water Tables                          |
| Generate Electricity | Solar                 | Land Area                             |
| Provide Shelter      | House                 | Land Area, Topography                 |
| Provide Shelter      | Garage                | Land Area, Topography                 |
| Provide Shelter      | Workshop              | Land Area, Topography                 |

> **Note:** Multiple subsystem technologies depend on geographies *land area* and *topography*

---

#### Economy

| Function                 | Implementation        | Dependency                         |
| ------------------------ | --------------------- | ---------------------------------- |
| Produce Food             | Agriculture           | Market Prices (operational upkeep) |
| Produce Food             | External Purchase     | Market Prices (food)               |
| Produce Water            | Precipitation Capture | Market Prices (operational upkeep) |
| Produce Water            | Well                  | Market Prices (operational upkeep) |
| Produce Water            | Municipal Supply      | Water Supply Cost                  |
| Generate Electricity     | Solar                 | Market Prices (operational upkeep) |
| Generate Electricity     | Utility Grid          | Electric Grid Cost                 |
| Provide Shelter          | House                 | Market Prices (operational upkeep) |
| Provide Shelter          | Garage                | Market Prices (operational upkeep) |
| Provide Shelter          | Workshop              | Market Prices (operational upkeep) |
| Control Climate          | HVAC                  | Market Prices (operational upkeep) |
| Control Climate          | Refrigerator          | Market Prices (operational upkeep) |
| Communication Connection | Internet              | Market Prices (operational upkeep) |
| Communication Connection | Phone Service         | Market Prices (operational upkeep) |
| Waste Management         | Plumbing              | Market Prices (operational upkeep) |
| Waste Management         | Recycling             | Market Prices (operational upkeep) |
| Waste Management         | Municipal Service     | Market Prices (operational upkeep) |

> **Note:** Majority of subsystem technology depends on economies *market prices* for operational upkeep

---

#### Shared Dependencies

| Dependency    | Dependent Technologies                       | Resource Domain(s)                                                      |
| ------------- | -------------------------------------------- | ----------------------------------------------------------------------- |
| Land Area     | Agriculture, Solar, Precipitation Capture    | Food, Electricity, Water                                                |
| Precipitation | Agriculture, Precipitation Capture, Well     | Food, Water                                                             |
| Market Prices | All except Municipal Supply and Utility Grid | Food, Electricity, Water, Shelter, Conditioned Environment, Information |

---

#### Result

Concept is feasible given:

* Climate has suitable *precipitation* levels
* Geography has enough *land area* and *topography* available
* Economies *market prices* for operational costs are within budget

These represent the dominant environmental constraints affecting multiple subsystem technologies.

---

### Stakeholder Compatibility

#### Affordability

| Technology            | Initial Cost          | Recurring Cost (annual)   |
| --------------------- | --------------------: | ------------------------: |
| Agriculture           | $                     | $                         |
| External Purchase     | -                     | $$                        |
| Precipitation Capture | $                     | $                         |
| Well                  | $$                    | $                         |
| Municipal Supply      | $                     | $                         |
| Solar                 | $$                    | $                         |
| Utility Grid          | $                     | $$                        |
| House                 | $$$                   | $$                        |
| Garage                | $$                    | -                         |
| Workshop              | $$                    | $                         |
| HVAC                  | $$                    | $                         |
| Refrigeration         | $                     | $                         |
| Internet              | $                     | $                         |
| Phone Service         | -                     | $                         |
| Plumbing              | $                     | $                         |
| Recycling             | -                     | $                         |
| Municipal Service     | $                     | $                         |
| **Total**             | $$$ + $$(5) + $(8)    | $$(4) + $(3)              |
| **Total (semantic)**  | *High Capital Burden* | *Moderate Capital Burder* |

**Grand Total:**

* High Capital Burden
* *hundreds of thousands of dollars*
* $$$(2)

> **Disclaimer:** Cost is based on imprecise, upper-bound approximations. Results should be used to gauge potential financial burden, not draw strict conclusions on economic feasibility.

**Rating Scale**

* *$* — Low Capital Burden (~$1,000 or *thousands of dollars*)
* *$$* — Moderate Capital Burden (~$10,000 or *tens of thousands of dollars*)
* *$$$* — High Capital Burden (~$100,000 or *hundreds of thousands of dollars*)
* *$$* = *$* × 10
* *\$\$\$* = *$$* × 10

---

#### Operational Coverage

| Resource                | Supporting Subsystem Technologies(s)           |
| ----------------------- | ---------------------------------------------- |
| Food                    | Agriculture, External Purchase                 |
| Water                   | Precipitation Capture, Well, Municipal Support |
| Electricity             | Solar, Utility Grid                            |
| Shelter                 | House, Garage, Workshop                        |
| Conditioned Environment | HVAC, Refrigeration                            |
| Information             | Internet, Phone Service                        |

---

#### Labor

TBD.

---

#### Result

* The selected subsystem technologies provide plausible mechanisms for satisfying stakeholder needs
* System upgrade cost is significant (~ *hundreds of thousands of dollars*) — cost optimizations must be thoroughly considered throughout system development life cycle to avoid exceeding budget
* System annual operational cost is roughly *tens of thousands of dollars* (~ equal to part-time income)

> **Disclaimer:** Quantitative analysis of cost must be made for a complete concept development.

---

### Compatibility Results

| Feasibility Criteria | Compatible? |
| -------------------- | ----------- |
| Technical            | ✓           |
| Environment          | ?           |
| Stakeholder          | TBD         |

* Environment compatibility depends on candidate selection
* Stakeholder compatibility is within the realm of feasible, though budget and labor must be thoroughly considered

---

## 4. Development Considerations

### Development Strategy

#### Architectural Principles

* Modular, scalable subsystem designs
* Incremental deployment
* Maintain compatibility with future subsystem expansion

#### Economic Priorities

* Prioritize technologies with low capital cost
* Prioritize technologies with short return on investment.
* Prioritize technologies with high resource production.

---

### Production Considerations

#### Availability of Materials

| Technology            | Commercial Availability |
| --------------------- | ----------------------- |
| Agriculuture          | ✓                       |
| Precipitation Capture | ✓                       |
| Well                  | ✓                       |
| Solar                 | ✓                       |
| House                 | ✓                       |
| Garage                | ✓                       |
| Workshop              | ✓                       |
| HVAC                  | ✓                       |
| Refrigeration         | ✓                       |
| Internet              | ✓                       |
| Phone Service         | ✓                       |
| Plumbing              | ✓                       |
| Recycling             | ✓                       |

---

#### Availability of Contractors

| Specialistis            | Availability |
| ----------------------- | ------------ |
| Algriculturists         | ✓            |
| Carpenters              | ✓            |
| Water Well Contractors  | ✓            |
| Solar System Installers | ✓            |
| Electricians            | ✓            |
| HVAC Contractors        | ✓            |

> **Note:** The above list is demonstrative rather than prescriptive.

---

#### Regulatory Concerns

**Agriculture:**

* Vary by state
* Building and Zoning permits (e.g., barns, greenhouses)
* Product-Specific licenses (for production farming)

**Precipitation Capture:**

* Vary by state
* Volume caps
* Permit requirements (primarily for large cisterns) 
* Usage limits (outdoor only, non-pottable)

**Well:**

* Well construction permit
* Licensed contractor
* Permit enforcements
* Water quality testing (recurring)

**Municipal Water Supply:**

* Planning that meets local codes
* Licenced contractors

**Solar:**

* Vary by state
* Safety standards (National Electric Code)
* Incentives (Investment Tax Credit)
* Net metering policies (for compensation on sell-back)
* Permit requirements (installation)

**Utility Grid:**

* Planning that meets local codes
* Inspection (via utility company)

**House / Garage / Workshop:**

* Local zoning laws
* Building permits

---

#### Construction Sequencing

1. Acquire property
2. Complete permitting and regulatory approvals
3. Establish essential utilities and supporting infrastructure
4. Construct primary resource production subsystems
5. Expand resource storage and resilience
6. Optimize system performance

---

### Risks

#### Shared Dependencies

##### Electricity 
Electricity failure can cause system wide disruption due to downstream reliance. The following subsystem technologies potentially rely on supporting electricity:

* Agriculture
* Precipitation Capture
* Well
* HVAC
* Refrigeration

##### Solar Radiation
Due to the significant role electricity plays in supporting system wide operations, solar radiation is an important climate variable that needs to be considered when selecting candidate properties. Backup technologies, such as *utility grid* and *generators* may be necessary for the sake of resilience.

##### Precipitation
A few major susystem technologies rely on precipitation for ongoing operational capacity:

* Agriculture
* Precipitation
* Well

##### Land Area
A sufficent amount of land area is needed for technology infrastructure to be productive:

* Agriculture
* Precipitation
* Solar

#### Verdict
While technical and resource compatibility is feasible, shared dependencies can cause system wide issues. Electricity, supporting three major resource domains (food, water, shelter), needs extra resilience to maintain operational capacity. Precipitation and land area also must be properly analyzed before conclusions are drawn due to supporting role they play in candidate technology performance.

---

## 5. Concept of Operations

The Home System is intended to maximize the utilization of locally produced resources while maintaining external infrastructure as supplemental or backup capacity. Resource production is prioritized according to cost, sustainability, and resilience, with external procurement used whenever local production cannot satisfy inhabitant demand.

---

### Normal Operation

Expected steady-state operations for daily inhabitance.

#### Food

Productive priority:

1. Agriculture – primary source
2. External Purchase — secondary source to meet unmet caloric needs

#### Water

Productive priority:

1. Precipitation Capture — primary source
2. Well — secondary supplementary source
3. Municipal Supply — backup source

#### Electricity

Productive priority:

1. Solar — primary source
2. Utility Grid — backup source

---

### Seasonal Operation

Seasonal operational variance.

---

#### Spring

| Technology                 | Operation(s)                                                              |
| -------------------------- | ------------------------------------------------------------------------- |
| Agriculture                | Preparations for outdoor cultivation                                      |
| External Purchase (food)   | Purchase of any food demand not stocked                                   |
| Precipitation Capture      | Increase in stocks                                                        |
| Well                       | Water table rises                                                         |
| Municipal Supply (water)   | Use for any demand not met                                                |
| Solar                      | Normal operational usage, Daylight increases                              |
| Utility Grid (electricity) | Use for any demand not met                                                |
| HVAC                       | Low usage, Maintenance and preparations of cooling unit for summer demand |

#### Summer


| Technology                 | Operation(s)                                                                         |
| -------------------------- | ------------------------------------------------------------------------------------ |
| Agriculture                | Peak production, Early harvesting begins, Increased irrigation needs                 |
| External Purchase (food)   | Purchase of any foods not provided by agriculture (e.g., meats, commercial products) |
| Precipitation Capture      | Low relative precipitation, Higer usage                                              |
| Well                       | Water table decreases and/or levels out, Higher usage, Potential to dry up           |
| Municipal Supply (water)   | Use as water stocks empty                                                            |
| Solar                      | Peak production, Higher usage due to HVAC and agricultural operation needs           |
| Utility Grid (electricity) | Use for any demand not met                                                           |
| HVAC                       | Heating unit not in use, High usage of cooling unit                                  |

#### Autumn

| Technology                 | Operation(s)                                                                                          |
| -------------------------- | ----------------------------------------------------------------------------------------------------- |
| Agriculture                | Final harvest, Food preservation                                                                      |
| External Purchase (food)   | Purchase of any foods not provided by agriculture (e.g., meats, commercial products)                  |
| Precipitation Capture      | Potential increase in precipitation, Lower relative usage, Replenish stocks, Clean storage containers |
| Well                       | Water tables replenished                                                                              |
| Municipal Supply (water)   | Use as necessary                                                                                      |
| Solar                      | Normal operational usage, Daylight decreases                                                          |
| Utility Grid (electricity) | Use for any demand not met                                                                            |
| Heat Pump                  | Low usage, Maintenance and preparations of heating unit for winter demand                             |

#### Winter

| Technology                 | Operation(s)                                                                |
| -------------------------- | --------------------------------------------------------------------------- |
| Agriculture                | Inactive or production reduced significantly                                |
| External Purchase (food)   | Purchase of any food demand not stocked                                     |
| Precipitation Capture      | Potential for snow and freeze conditions, Snow melting                      |
| Well                       | Issues with infrastucture freezing                                          |
| Municipal Supply (water)   | Use for any demand not met, Higher usage (based on stakeholder water usage) |
| Solar                      | Production low, Daylight at low                                             |
| Utility Grid (electricity) | Use for any demand not met                                                  |
| Heat Pump                  | High usage of heating unit, Cooling unit not in use                         |

---

### Human Participation

#### Daily

* Monitor resource availability
* Consume produced resources
* Perform minor inspections as necessary

#### Weekly

* Garden maintenance
* Harvest mature crops
* Monitor stored resources

#### Seasonal

* Plant crops
* Preserve food
* Prepare systems for seasonal transition

#### Abnormal

* Repair damaged infrastructure
* Expand productive capacity
* Replace failed equipment

---

### Maintenance Concept

#### Routine

* Cleaning
* Inspection
* Minor repairs

#### Preventive

* Seasonal servicing
* Infrastructure inspection
* Consumable replacement

#### Corrective

* Repair failed subsystems
* Replace damaged infrastructure

#### Long-Term

* Replace end-of-life equipment
* Expand productive capacity

---

### Abnormal Operation

#### Power Outage

* Solar remains primary source of electricity
* Backup (utility grid) is lost
* Resilience is severely effected (due systemic dependence on electric)

#### Drought

* Water stocks from precipitation run out
* Water tables become an unstable source
* Agricultural irrigation demands may become unmet, causing decrease in food production
* Municipal supply becomes primary source of water

#### Operator Illness

* Agricultural system may not receive full labor needs reducing overall harvest

---

## 6. Evaluation Strategy

* Annual food production
* Annual water production
* Annual electrical generation
* Operating cost ($)
* Labor hours

---

## 7. Feasible System Concept

The proposed Home System consists of modular agricultural, water, electrical, and environmental control subsystems intended to maximize local resource production while maintaining external infrastructure as supplemental capacity. Technical compatibility analysis indicates subsystem interfaces are realizable. Environmental analysis indicates feasibility is conditional upon adequate precipitation, land area, and solar availability. Stakeholder analysis indicates implementation appears economically achievable through incremental development. The concept is therefore considered suitable for feasibility validation through operational simulation and quantitative performance analysis.
