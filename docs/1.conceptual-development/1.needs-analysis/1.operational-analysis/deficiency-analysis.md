# Deficiency Analysis

## Current System

**Attributes:**
* Area: 1/4 acre
* Precipitation (annual): 49 in
* Growing Season Length: 6 months (April - October)
* Solar Radiation: 4.33 kWh

---

### Inhabitant Demand

**Caloric intake:**
* 13000 kcal/day
* 395417 kcal/month
* 4745000 kcal/year

**Water usage / consumption:**
* 213 gallons/day
* 6483 gallons/month
* 10400 gallons/year

**Energy usage:**
* 47 kWh/day
* 1417 kWh/month
* 17000 kWh/year

**Shelter:** ~2000 ft² of living area

**Conditioned Environment:** 65-85 °F

**Information:**

* Download throughput — ≥50 Mbps
* Upload throughput — ≥10 Mbps
* Latency — ≤50 ms
* Jitter — ≤20 ms
* Packet loss — ≤0.5%
* Response time — ≤1 s

> **Disclaimer:** With the exception of *water usage*, all values are based on conservative estimations of a household with 4-6 inhabitants.

---

### Land Capacity

**Agricultural yield:** ~2000 calories/annually

**Water yield:** 0 gallons

**Energy Yield:** 0 kWh

---

## Deficiency Report

* Very low production output
* Insignificant agricultural output relative to demand
* Likely a relatively significant ceiling for improvement considering modern infrastructural capabilities (e.g., solar, water capture, etc.)

---

## Notes

### Information Performance Benchmarks (Internet)

| Metric                   | Typical Residential |  Acceptable | Minimum Effective |
| ------------------------ | ------------------: | ----------: | ----------------: |
| Download throughput      |        100–500 Mbps | 25–100 Mbps |        10–25 Mbps |
| Upload throughput        |         10–100 Mbps |   5–20 Mbps |          2–5 Mbps |
| Latency (RTT)            |            10–30 ms |      <50 ms |           <150 ms |
| Jitter                   |              1–5 ms |      <20 ms |            <30 ms |
| Packet loss              |                  0% |       <0.5% |               <1% |
| Response time (page/app) |          100–500 ms |        <1 s |            <2–3 s |

#### Throughput

| Activity                    |              Recommended |
| --------------------------- | -----------------------: |
| Email                       |                  <1 Mbps |
| Instant messaging           |                  <1 Mbps |
| iCloud sync (background)    |                 1–5 Mbps |
| HD video call               | 3–5 Mbps both directions |
| 4K streaming                |               15–25 Mbps |
| Multiple simultaneous users |              50–100 Mbps |

#### Latency

|        RTT | Experience                       |
| ---------: | -------------------------------- |
|     <20 ms | Excellent                        |
|   20–50 ms | Very good                        |
|  50–100 ms | Acceptable                       |
| 100–150 ms | Noticeable delay                 |
|    >150 ms | Poor for real-time communication |

#### Jitter

|   Jitter | Experience                  |
| -------: | --------------------------- |
|    <5 ms | Excellent                   |
|  5–10 ms | Very good                   |
| 10–20 ms | Acceptable                  |
| 20–30 ms | Minor audio/video artifacts |
|   >30 ms | Frequent stuttering         |

#### Packet Loss

|   Loss | Experience                                 |
| -----: | ------------------------------------------ |
|     0% | Ideal                                      |
|  <0.1% | Excellent                                  |
|  <0.5% | Very good                                  |
| 0.5–1% | Generally usable                           |
|   1–2% | Noticeable interruptions                   |
|    >2% | Poor                                       |
|    >5% | Nearly unusable for real-time applications |

#### Response Time

| Response time | Experience          |
| ------------: | ------------------- |
| 100-300 ms    | Feels instantaneous |
| 300-800 ms    | Responsive          |
| 0.8-2 s       | Acceptable          |
| 2-5 s         | Slow                |
| >5 s          | Frustrating         |