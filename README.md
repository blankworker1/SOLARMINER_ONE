# SOLARMINER_ONE

An Open-Source Platform for Studying Solar-Powered Computation

---

## Contents

- [SolarMiner One](#solarminer-one)
  - [Overview](#overview)
  - [Research Concept](#research-concept)
  - [The Complete Process](#the-complete-process-physical-layer)
  - [System Architecture](#system-architecture)
    - [Hardware Layer](#hardware-layer)
    - [Monitoring & Control Layer](#monitoring--control-layer)
    - [Data Logging & Storage Layer](#data-logging--storage-layer)
  - [What We Aim to Study](#what-we-aim-to-study)
  - [Key Metrics](#key-metrics)
  - [Open Participation](#open-participation)
  - [Getting Started](#getting-started)
  - [What SolarMiner One Is Not](#what-solarminer-one-is-not)
  - [Future Directions](#future-directions)
  - [Status](#status)
 
    
## Overview

SolarMiner One is an open-source hardware, software, and data-collection platform built entirely from off-the-shelf components. Its goal is to enable a distributed, reproducible research network that studies how solar energy availability translates into real computational work under different environmental and regulatory conditions.

At its first stage, SolarMiner One is positioned as a pan-European research project, open to individuals, institutions, and citizen scientists who wish to deploy identical nodes and share standardized data.

The project intentionally avoids proprietary hardware, cloud dependencies, or opaque metrics. Instead, it focuses on measuring reality: how much useful computation can be performed when powered directly by small-scale solar generation.


---

## Research Concept

Each SolarMiner One node is an identical, grid-connected, solar-powered computational unit. Nodes are deployed in different European locations and operated continuously over long periods.

The project studies how local climate, seasonality, geography, and regulatory context affect:

Solar energy availability

System operating behavior

Computational work output


The result is a standardized, comparable, long-term dataset designed for reuse beyond the lifetime of any single study or grant.


---

## The Complete Process

At the most fundamental level, SolarMiner One measures a closed physical process:
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

This end-to-end chain provides a unique, externally validated measure of how renewable energy availability maps to real computation.


---

## System Architecture

SolarMiner One is organized into three clearly separated layers.


### 1. Hardware Layer

(Energy and Computation)

This layer represents the physical process itself.

Solar PV panel (balcony-scale, grid-connected)

Micro-inverter

Small, fixed-power computational device (Bitaxe class)

Grid connection for stability and smooth operation


This layer answers the question:

> How much computation can be performed from locally available solar energy?

---

### 2. Monitoring & Control Layer

(Local Observability)

This layer observes system behavior without adding complexity or user interaction.

It includes:

PV and inverter power monitoring

System power consumption monitoring

Device operating state

Optional panel-adjacent temperature sensing
(air temperature behind the PV panel, measured via a simple outdoor sensor)


This layer provides context, not control.
The system is designed to operate autonomously.

--- 

### 3. Data Logging & Storage Layer

(Long-Term Research Data)

Data is collected and stored at two levels:

Local storage on the node (Home Assistant)

Remote archival storage (research database)


Characteristics:

Long-term time-series data

Standardized schema across all nodes

No cloud lock-in

Designed for cross-site comparison and seasonal analysis


The user dashboard remains minimal; most data is collected silently for research purposes.


---

## What We Aim to Study

The project focuses on answering concrete, measurable questions:

Seasonal variation
How does computational output vary across the year?

Geographic effects
How do latitude and regional conditions affect solar-powered computation?

Climatic effects
How do temperature and local conditions influence system efficiency?

Energy → computation efficiency
How much usable computation is produced per unit of solar energy?

Solar availability vs work output
How closely does real-world solar generation map to sustained computational work?

---

## Key Metrics

SolarMiner One nodes collect a minimal, standardized set of primary and derived metrics designed to enable direct cross-site comparison without calibration-heavy instrumentation. All measurements are timestamped and stored in a unified time-series database.

The platform deliberately prioritizes system-observable metrics over inferred or externally sourced data.

**Energy Metrics**

PV panel instantaneous AC power output (W)

Daily, weekly, and cumulative solar energy generation (kWh)

Grid energy import/export (kWh) for net energy balance

System instantaneous power consumption (W)

Computational device power draw (W)

Note: PV power output is used as a practical proxy for solar availability; no dedicated irradiance sensor is required.

**Environmental Metrics**

Panel-adjacent air temperature (°C)

Note: Environmental data is collected silently for research purposes and is not exposed in the user dashboard.

**Computation Metrics**

Hash rate (H/s) as a standardized computational workload

Accepted work units (per time period)

Uptime / downtime periods

Thermal characteristics of the computational device

Estimated sats earned (per period and cumulative)

**Derived Metrics**

Energy-to-computation efficiency (H/s per Watt)

Solar availability vs work output correlation

Seasonal performance variation

Geographic performance indices

Net energy surplus / deficit over time

Long-term operational stability metrics

All metrics follow a standardized schema across nodes, ensuring direct comparability without normalization or site-specific tuning.

---

## Open Participation

SolarMiner One is designed to be:

Open source (hardware definitions, software configuration, data schema)

Replicable using commercially available components

Accessible to individuals, universities, labs, and community groups


Anyone can:

- Build a SolarMiner One node

- Contribute data

- Run independent analyses

- Propose extensions or variants


All participants operate identical reference systems to ensure comparability.

---

## Getting Started 

Deploying a SolarMiner One node requires basic technical competence, but no specialized solar, cryptographic, or data-science expertise. The process is designed to be reproducible across different European locations.

**Prerequisites**

Basic electrical safety awareness

Home networking familiarity

Ability to follow documented installation steps

Access to a suitable balcony or installation location with solar exposure

**Hardware Acquisition**

Verify compatibility with local electrical standards

Confirm grid-connection legality for balcony PV in your jurisdiction

Procure components from the validated, off-the-shelf hardware list (link)


**Installation Process**

Mount the PV panel and connect the micro-inverter

Connect the inverter and system to the grid via approved outlets

Install the computational device inside the SolarMiner enclosure

Mount the panel-adjacent temperature sensor behind the PV panel

Connect the system to the local internet network

**Software Deployment**

Power on the pre-configured system

Verify automatic initialization of monitoring services

Assign node-specific metadata (location ID, timezone)

Confirm data logging locally and transmission to the remote research database

Validate dashboard visibility via the companion tablet or browser

**Verification Checklist**

PV power data visible and updating

System power consumption correctly measured

Computational workload running and reporting

Data appearing in local logs and remote archive

Node status stable over a 24-hour cycle


---

## What SolarMiner One Is Not

Not a commercial mining product

Not a financial instrument

Not a proprietary platform

Not a cloud-dependent service


Bitcoin mining is used strictly as a globally verifiable, deterministic workload and accounting mechanism for computational work.


---

## Future Directions

Future versions may include:

Expanded geographic participation

Longitudinal, multi-year datasets

Off-grid experimental variants (separate specification)

Academic publications and policy-relevant analysis


These are intentionally out of scope for the initial reference platform.


---

## Status

SolarMiner One is currently in its reference implementation and pilot deployment phase.

The immediate goal is to:

Validate the platform

Finalize the data schema

Deploy multiple identical nodes across Europe

Begin long-term data collection



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

## Reference Hardware (Proof of Concept)

**Internal**

- Bitaxe Miner – NerdQAxe+ (~90 W)

Wi-Fi connected

Built-in temperature monitoring (via API)


- Home Assistant Green

Headless operation

Ethernet connected to local router

Preconfigured dashboard and automations


- Enclosure

Desktop form factor

Ventilated

Grounded



**External**

- Solar Panel

400–500 W typical


- Micro-Inverter

Example: Hoymiles HMS-800W-2T (balcony PV)


- Monitoring

Shelly Plug Gen3 (PV output monitoring)

Shelly Plug Gen3 (system power monitoring)

Shelly H&T (temperature and humidity monitoring)


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

## Philosophy

> SolarMiner One turns sunlight into verifiable work, and records what actually happens.






