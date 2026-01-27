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

**Local Storage**

Home Assistant Recorder

Long-term statistics engine

Retention configurable per deployment

Designed for multi-year operation


**Remote Data Upload (Optional)**

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

The Data Block is a headless appliance. All configuration, monitoring, and interaction are performed via the Home Assistant Companion App on a tablet or mobile device.

No keyboard, mouse, or display is required.


---

## Initial Setup (Local Network)

1. Power on the Home Assistant Green


2. Connect the device to the local router via Ethernet


3. Install the Home Assistant Companion App on a tablet or phone


4. Ensure the tablet/phone is connected to the same local network


5. Open the Companion App and complete Home Assistant onboarding


6. Assign:

System name

Location metadata

Timezone




At this stage, the Data Block is fully operational on the local network.


---

## Integration Setup

Using the Companion App:

1. Install required integrations:

Shelly (Load Block power telemetry)

Miner integration (AxeOS / REST)

MQTT (Gateway Block solar data)

OpenDTU integration (via MQTT)


2. Verify automatic discovery of:

Load Block devices

Gateway Block devices


3. Assign consistent node identifiers for research tracking


All configuration is performed via the app UI; no YAML editing is required for standard deployments.


---

## Remote Access & Management

The Data Block supports secure remote access using Tailscale.

1. Install and start the Tailscale Add-on on Home Assistant


2. Authenticate the device to the project tailnet


3. Install the Tailscale app on the tablet/phone


4. In the Home Assistant Companion App:

Set Internal URL to the local HA address

Set External URL to the Tailscale IP of Home Assistant

The app automatically switches between local and remote access based on network availability.


---

## Optional Remote Data Export

If enabled, the Data Block can stream data to a remote research database:

1. Configure the InfluxDB integration

2. Point to the remote database over Tailscale

3. Enable periodic or continuous upload

This process is outbound-only and does not affect local visualization or automation.

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


Public facing dashboards are non-interactive by design, optimized for periodic review rather than active control.

---

## Normal Operation

Once configured:

The Data Block runs unattended

Dashboards update automatically

Automations execute locally

Data is stored long-term and optionally exported


No daily interaction is required.


---

## Recovery & Maintenance

Power cycling the Home Assistant Green is safe

Configuration persists across reboots

Remote access remains available after restarts

Updates can be applied remotely via the Companion App.

---

## Design Principles

Centralized analysis, decentralized operation

No single point of failure

Outbound-only connectivity

Open data formats and schemas

Reproducible configuration



---

## Summary

The Data Block requires only local network access during initial setup. After provisioning, it can be monitored and managed entirely via the Home Assistant Companion App, both locally and remotely, without physical access to the hardware.

This headless design supports scalable, multi-site deployment while keeping user interaction minimal and consistent across installations.

The Data Block is the analytical core of OpenSolar One. It unifies solar input, environmental context, and computational output into a coherent, long-term dataset suitable for scientific analysis, comparative studies, and public research.

While logically central, the Data Block is not operationally critical to the Gateway or Load Blocks, preserving system robustness and measurement integrity.

The Data Block specification is stable for OpenSolar One v1 and supports aggregation from multiple geographically distributed nodes.










