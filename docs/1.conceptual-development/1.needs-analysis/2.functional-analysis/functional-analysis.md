# Functional Analysis

- [Functional Analysis](#functional-analysis)
  - [Functional Elements](#functional-elements)
    - [Capital](#capital)
    - [Labor](#labor)
    - [Resources](#resources)
    - [Food](#food)
    - [Water](#water)
    - [Electricity](#electricity)
    - [Shelter](#shelter)
    - [Conditioned Environment](#conditioned-environment)
    - [Information](#information)
  - [System Environment](#system-environment)
    - [Climate](#climate)
    - [Geography](#geography)
    - [Economy](#economy)
  - [Subsystem Functions](#subsystem-functions)
    - [Produce Food](#produce-food)
    - [Produce Water](#produce-water)
    - [Generate Electricity](#generate-electricity)
    - [Provide Shelter](#provide-shelter)
    - [Control Climate](#control-climate)
    - [Store Resource](#store-resource)
    - [Communication Connection](#communication-connection)
    - [Waste Management](#waste-management)
  - [Subsystem Flows](#subsystem-flows)
    - [Food](#food-1)
    - [Water](#water-1)
    - [Electricity](#electricity-1)
    - [Conditioned Environment](#conditioned-environment-1)

---

*`Home(Capital, Labor, Resources) → { Food, Water, Electricity, Shelter, ConditionedEnvironment, Information }`*

## Functional Elements

| Input/Output            | Element          |
| ----------------------- | ---------------- |
| Capital                 | Material, Signal |
| Labor                   | Material, Energy |
| Resources               | TBD              |
| Food                    | Material, Energy |
| Water                   | Material, Energy |
| Electricity             | Energy           |
| Shelter                 | Material         |
| Conditioned Environment | Energy           |
| Information             | Data, Signal     |

---

### Capital

* Corresponds to intial investment and any overhead cost (e.g, operational, maintenance)
* *Material* when determining resource capacity (e.g., *$100 → x amount lumber*)
* *Signal* when making economic decisions

| Element  | Units | Example                                                   |
| -------- | ----- | --------------------------------------------------------- |
| Material | $     | Initial investment, Cost of materials                     |
| Signal   | $     | Trade-off variable (e.g, price of solar vs hydro vs wind) |

---

### Labor

* The amount of caloric expenditure or time maintaining operational tasks
* *Material* when viewed as time
* *Energy* when viewed as expenditure or *work*

| Element  | Units        | Example                                        |
| -------- | ------------ | ---------------------------------------------- |
| Material | hours, days  | Amount of time spent maintaining garden        |
| Energy   | kilocalories | Amount of energy expended to process dry beans |

---

### Resources

* A placeholder abstraction for any non-capital / non-labor, implementation-specifc input required by home systems to perform operational tasks (e.g., infrastructure, seeds, climate, etc.)

---

### Food

* *Material* when viewed as storage space needs
* *Energy* when viewed as metabolic demand

| Element  | Units             | Example                                             |
| -------- | ----------------- | --------------------------------------------------- |
| Material | ft³, gallons, lbs | Yield in lbs, 10 gallons of potato stored           |
| Energy   | kilocalories      | Caloric yield, Caloric support of inhabitant demand |

---

### Water

* *Material* when viewed as storage space needs
* *Energy* when viewed as metabolic demand

| Element  | Units                | Example                                                                   |
| -------- | -------------------- | ------------------------------------------------------------------------- |
| Material | ft³, gallons, lbs    | Yield in lbs, 5000 gallons of storage space                               |
| Energy   | gallons, fl oz, cups | Hydration needs, Inhabitant needs 8 cups daily to support survival demand |

---

### Electricity

* *Energy* element representing power needs over time

| Element  | Units | Example                            |
| -------- | ----- | ---------------------------------- |
| Energy   | kWh   | Home requires ~17,000 kWh annually |

---

### Shelter

* Physical structures that protect occupants and assets from the external environment
* *Material* when viewed as physical structure or substance (e.g, house, insulation, temperate air, etc.)

| Element  | Units                       | Example                               |
| -------- | --------------------------- | ------------------------------------- |
| Material | ft, ft³, lbs, gallons, etc. | 2000 sq ft house, 200 lbs of concrete |

---

### Conditioned Environment

* Any aspect of home system which participates regulating climate and environment
* *Material* when viewed as a physical substance (e.g, temperate air, etc.)
* *Energy* when viewed as thermoregulatory needs (thermal energy)

| Element  | Units                       | Example                               |
| -------- | --------------------------- | ------------------------------------- |
| Material | ft, ft³, lbs, gallons, etc. | Cooling capacity of air conditioner   |
| Energy   | degrees (°)                 | Interior space must remain under 72°F |

---

### Information

* Any element which provides insights or stores knowledge
* *Data* when information is stored or otherwise observed
* *Signal* when information influences decisions or otherwise effects change

| Element  | Units                    | Example                                   |
| -------- | ------------------------ | ----------------------------------------- |
| Data     | GB, Mbps, messages, etc. | 500 Mbps throughput                       |
| Signal   | TBD                      | Price point, Temperature, Solar Radiation |

---

## System Environment

* Climate
* Economy
* Geography

> **Disclaimer:** The following definitions are non-exhaustive and demonstrative rather than nor prescriptive.

---

### Climate

```text
Climate = {
    Precipitation,
    Temperature,
    Humidity,
    Aridity,
    Solar Radiation,
    Growing Season Length,
    Frost Frequency,
    Wind
}
```

---

### Geography

```text
Geography = {
    Land Area,
    Soil Viability,
    Water Tables,
    Water Bodies,
    Topography
}
```

---

### Economy

```text
Economy = {
    Electric Grid Cost,
    Municipal Water Cost,
    Food Prices,
    Property Taxes,
    Local Income
}
```

---

## Subsystem Functions

* Produce Food
* Produce Water
* Generate Electricity
* Provide Shelter
* Control Climate
* Store Resource
* Communication Connection
* Waste Management

> **Disclaimer:** All listed dependencies are speculative. Implementation design may vary.

---

### Produce Food

*`ProduceFood(Capital, Labor, Resources) → Food`*

| Potential Implementation | Potential Dependencies                                                                        |
| ------------------------ | --------------------------------------------------------------------------------------------- |
| Agriculture              | Water, Electricity, Conditioned Environment (indoor agriculture), Climate, Geography, Economy |
| Domestic Livestock       | Water, Electricity, Food, Conditioned Environment, Climate, Geography, Economy                |
| Game / Hunting           | Geography, Economy                                                                            |
| Externally Sourced       | Economy                                                                                       |

---

### Produce Water

*`ProduceWater(Capital, Labor, Resources) → Water`*

| Potential Implementation | Potential Dependencies                   |
| ------------------------ | ---------------------------------------- |
| Precipitation Capture    | Electricity, Climate, Geography, Economy |
| Well                     | Electricity, Climate, Geography, Economy |
| Water Bodies             | Climate, Economy                         |
| Municipal Supply         | Economy                                  |

---

### Generate Electricity

*`GenerateElectricity(Capital, Labor, Resources) → Electricity`*

| Potential Implementation | Potential Dependencies      |
| ------------------------ | --------------------------- |
| Solar                    | Climate, Geography, Economy |
| Hydro                    | Climate, Economy            |
| Wind                     | Climate, Geography, Economy |
| Mechanical               | Economy                     |
| Utility Grid             | Economy                     |

---

### Provide Shelter

*`ProvideShelter(Capital, Labor, Resources) → Shelter`*

| Potential Implementation | Potential Dependencies      |
| ------------------------ | --------------------------- |
| House                    | Geography, Economy          |
| Barn                     | Geography, Economy          |
| Garage                   | Geography, Economy          |

---

### Control Climate

*`ControlClimate(Capital, Labor, Resources) → ConditionedEnvironment`*

| Potential Implementation | Potential Dependencies      |
| ------------------------ | --------------------------- |
| HVAC                     | Electricity, Economy        |
| Refrigeration            | Electricity, Economy        |

---

### Store Resource

*`StoreResource(Capital, Labor, Resources) → Resource`*

| Potential Implementation | Potential Dependencies                                                            |
| ------------------------ | --------------------------------------------------------------------------------- |
| Food Preservation        | Electricity, Shelter, Water, Conditioned Environment, Climate, Geography, Economy |
| Water Storage            | Electricity, Conditioned Environment, Climate, Geography, Economy                 |
| Energy Storage           | Shelter, Conditioned Environment, Climate, Geography, Economy                     |

---

### Communication Connection

*`CommunicationConnection(Capital, Labor, Resources) → Information`*

| Potential Implementation | Potential Dependencies                   |
| ------------------------ | ---------------------------------------- |
| Internet                 | Electricity, Climate, Geography, Economy |
| Phone Service            | Electricity, Climate, Geography, Economy |

---

### Waste Management

*`WasteManagement(Capital, Labor, Resources)`*

| Potential Implementation | Potential Dependencies      |
| ------------------------ | --------------------------- |
| Plumbing                 | Water, Economy              |
| Recycling                | Economy                     |
| Municipal Service        | Economy                     |

---

## Subsystem Flows

### Food

* **Food** : *Energy* → **Food** (Domestic Livestock)

---

### Water

* **Water** : *Energy* →
  * **Food** (Agriculture, Domestic Livestock)
  * ∧ **Resource Surplus** (Food Presevation)
* **Water** : *Material | Energy* → **Removal** (Plumbing)

---

### Electricity

* **Electricity** : *Energy* → 
  * **Food** (Agriculture, Domestic Livestock)
  * ∧ **Water** (Precipitation Capture, Well)
  * ∧ **Conditioned Environment** (HVAC, Refrigeration)
  * ∧ **Resource Surplus** (Food Presevation, Water Storage, Energy Storage)
  * ∧ **Information** (Internet, Phone Service)

---

### Conditioned Environment

* **Conditioned Environment** : *Material | Energy* →
  * **Food** (Indoor Agriculture, Domestic Livestock)
  * ∧ **Resource Surplus** (Food Presevation, Water Storage, Energy Storage)
