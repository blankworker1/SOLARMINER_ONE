# DATA BLOCK

## Overview

The Data Block is the central coordination, analysis, and archival component of the OpenSolar One platform. It aggregates standardized telemetry from one or more Gateway and Load Blocks, calculates primary research metrics, and maintains both local and long-term datasets.

The Data Block is logically central but functionally independent. Gateway and Load Blocks continue operating autonomously if the Data Block is offline, ensuring resilience and data continuity at the edge.


---

## Functional Role

The Data Block answers the core synthesis question of the project:

> How efficiently is solar energy converted into verifiable computational work across time and geography?



It provides:

Unified system state and visualization

Cross-block metric correlation

Long-term data logging and export

Secure remote access and management



---

## Hardware Architecture

Core Components

**Home Assistant Green**

Dedicated appliance for automation and monitoring

Runs Home Assistant OS (headless)

Hosts dashboards, integrations, and automation logic

Provides long-term statistics and data retention


**Power Supply**

Supplied AC→DC adapter (12 V DC)

Typical power draw <10 W

Designed for continuous operation




---

## Electrical Characteristics

Component	Typical Power	Notes

Home Assistant Green	5–8 W	(dependent on integrations)

Power Adapter	12 V DC	Supplied unit


The Data Block’s power consumption is intentionally minimal and independent of the Gateway and Load Blocks.


---

## Connectivity

Home Assistant Green → Network

Ethernet - LAN cable to local router 

Ensures stable, low-latency connectivity

Avoids Wi-Fi variability for central coordination


## Secure Remote Access

Tailscale add-on provides encrypted peer-to-peer connectivity

No inbound ports or router configuration required

The Data Block can be deployed on-site or at a remote location.


---

## Data Ingestion

The Data Block ingests data directly from each block:

**From Gateway Block**

PV generation (W, Wh)

Inverter telemetry

Environmental measurements

Solar-side system status


**From Load Block**

Miner hashrate and thermal data

Power consumption (W, Wh)

Operational state and uptime


Each block reports independently; no block acts as a relay for another.


---

## Data Storage & Retention

Local Storage

Home Assistant Recorder

Long-term statistics engine

Retention configurable per deployment

Designed for multi-year operation


Remote Data Upload (Optional)

The Data Block supports optional, automated export to a remote research database:

InfluxDB (v2) recommended

Secure transport via Tailscale

Periodic or continuous upload

Suitable for:

Multi-site aggregation

Longitudinal analysis

Public or consortium datasets


Export operates outbound-only and does not affect local operation.


---

## Configuration & Provisioning

Provisioning is minimal and performed once.

1. Power on Home Assistant Green


2. Complete initial HA onboarding


3. Install required integrations:

Shelly

REST / Miner integration

OpenDTU / MQTT

Tailscale add-on



4. Authenticate Tailscale to join the project tailnet


5. Assign node identifiers for connected Gateway and Load Blocks



All ongoing configuration and monitoring is performed remotely.


---

## Dashboards & Automations

The Data Block hosts:

A minimalist status dashboard

Long-term energy and computation metrics

Health and availability indicators


Automations may include:

Miner restart on fault detection

Status classification (sun / star / paused)

Data integrity checks


Dashboards are non-interactive by design, optimized for periodic review rather than active control.


---

## Design Principles

Centralized analysis, decentralized operation

No single point of failure

Outbound-only connectivity

Open data formats and schemas

Reproducible configuration



---

## Summary

The Data Block is the analytical core of OpenSolar One. It unifies solar input, environmental context, and computational output into a coherent, long-term dataset suitable for scientific analysis, comparative studies, and public research.

While logically central, the Data Block is not operationally critical to the Gateway or Load Blocks, preserving system robustness and measurement integrity.

The Data Block specification is stable for OpenSolar One v1 and supports aggregation from multiple geographically distributed nodes.










