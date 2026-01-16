# SOLARMINER_ONE

Solar powered ASIC node and monitoring/control platform

---

## An Open Reference Platform for Solar-Powered Computation

SolarMiner One is an open-source hardware and software project that enables anyone to assemble a small, standardized, solar-powered computational node and contribute long-term, comparable telemetry data.

The project uses solar photovoltaic energy to perform verifiable cryptographic work (Bitcoin proof-of-work) and records the relationship between energy availability, computation, and output over time.

This is not primarily a mining product.

It is a distributed instrumentation platform built on real physics.


---

## Project Goals

The primary goals of SolarMiner One are:

- Enable reproducible, open hardware builds

- Provide standardized data collection

- Capture long-term, real-world telemetry

- Allow global comparison across geography and seasons

- Preserve user autonomy and transparency


Profitability, optimization, and yield are explicitly secondary.


---

## What SolarMiner One Is

A reference hardware configuration

A preconfigured Home Assistant environment

A solar-powered computation node

A standard telemetry emitter

A local-first system with optional data sharing


Each SolarMiner One node converts incident solar radiation into electrical energy, uses that energy to perform cryptographic computation, and records the resulting physical and computational data.


---

## What SolarMiner One Is Not

Not a cloud service

Not a black-box appliance

Not a “get rich quick” miner

Not a proprietary ecosystem

Not a battery-based energy system


SolarMiner One relies on grid-connected operation for stability and repeatability.


---

## System Overview

```

Sunlight (photons)

        ↓
        
Solar PV Panel

        ↓
        
Micro-Inverter (grid-connected)

        ↓
        
Electrical Power (AC)

        ↓
        
Bitaxe Miner (computation)

        ↓
        
Cryptographic Work

        ↓
        
Satoshis (via mining pool)

```

In parallel, all relevant telemetry is captured and logged.


---

## Reference Hardware (Proof of Concept)

**Internal**

- Bitaxe Miner – NerdQAxe+ (~90 W)

Wi-Fi connected

Built-in temperature monitoring (via API)


- Home Assistant Green

Headless operation

Ethernet connected to local router

Preconfigured dashboard and automations


- Cooling System

5 V USB fan

Wi-Fi USB switch

Fan control driven by Bitaxe temperature data


- Enclosure

Desktop form factor

Ventilated

Grounded



**External**

- Solar Panel

400–500 W typical


- Micro-Inverter

Example: Hoymiles HMS-800W-2T (balcony PV)


- Smart Power Monitoring

Shelly Plug Gen3 (PV output monitoring)

Shelly Plug Gen3 (system power monitoring)


- Tablet

Runs Home Assistant Companion app

Primary user interface

All hardware can be sourced locally.


---

## Dashboard Philosophy

The SolarMiner dashboard is:

Minimalist

Non-interactive

Calm

Worth checking once per day


The dashboard answers three questions:

1. Is the system healthy?


2. Is it daytime or nighttime operation?


3. Is work being performed as expected?



Status Indicators

☀️ Sun — PV power exceeds system power (persistent)

⭐ Star — System in nighttime/standby (persistent)

⚠️ Triangle — Fault or unavailable state


Transient fluctuations (clouds, dawn/dusk) are suppressed using persistence logic.


---

## Data Collection

SolarMiner One records:

Physical Metrics

PV output power

System power consumption

Temperature (miner and environment)

Uptime and duty cycles


Computational Metrics

Hashrate

Miner state

Thermal throttling


Economic Metrics

Satoshis mined per day (estimated)

Total sats mined per node



---

## Long-Term Data & Research

Each node can optionally stream standardized telemetry to a remote database using:

Tailscale (peer-to-peer VPN)

InfluxDB (time-series storage)


Data is:

Local-first

User-controlled

Uploaded periodically (e.g. monthly)

Structured for aggregation and comparison


The long-term aim is to study:

Seasonal variation

Geographic effects

Energy → computation efficiency

Solar availability vs work output



---

## Open Source Commitment

SolarMiner One is:

Open hardware

Open firmware

Open dashboards

Open data schemas


Users are free to:

Modify

Fork

Extend

Analyze

Opt out of data sharing


Transparency is a requirement, not a feature.


---

## Who This Project Is For

Builders and tinkerers

Researchers

Energy nerds

Bitcoin protocol enthusiasts

Anyone curious about solar-powered computation



---

## Getting Started

1. Assemble reference hardware


2. Install Home Assistant configuration


3. Connect PV and power monitoring


4. Verify dashboard status


5. (Optional) Enable remote data streaming



Detailed build and configuration guides are provided in /docs.


---

## Contributing

Contributions are welcome in the form of:

Documentation

Data schema refinement

Hardware variants

Analysis tools

Visualization improvements


If you can reproduce it, measure it, or explain it better — it belongs here.


---

## Philosophy (In One Sentence)

> SolarMiner One turns sunlight into verifiable work, and records what actually happens.






