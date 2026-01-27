# GATEWAY BLOCK


## Overview

The Gateway Block is a self-contained, outdoor-rated integration hub designed to bridge local solar production hardware with a centralized Home Assistant–based research platform. It performs three critical roles:

- Capture proprietary telemetry from Hoymiles microinverters

- Aggregate solar, environmental, and power data locally

- Transmit standardized metrics securely to a remote Data Block (Home Assistant Green)

The Gateway Block is designed for zero-touch deployment, no cloud dependencies, and fully autonomous operation once installed. 

---

## Hardware - Core Components

**Raspberry Pi Zero 2 W** - acts as the gateway brain and local server. Selected for:

Low and stable power consumption

Sufficient CPU and RAM headroom for MQTT, VPN, and future expansion (camera, sensors)

Integrated Wi-Fi for client and AP provisioning modes

---

**OpenDTU Fusion** - ESP32-S3 based device that:

Communicates directly with Hoymiles microinverters via Sub-1GHz RF

Decodes proprietary inverter telemetry

Publishes structured data via MQTT over local Wi-Fi

---

**Shelly H&T** - wifi humidity and temperature sensor. Installed inside the enclosure to:

Monitor internal temperature and humidity

Provide early warning of thermal or condensation issues

Operate from USB power (no batteries)

---

**Power Supply** - 5V USB, 240v mains, high-quality, isolated PSU powering:

Raspberry Pi Zero 2 W

OpenDTU Fusion

USB-powered sensors

---

**Weatherproof Enclosure** - configured as an inline adapter module with:

Short Schuko AC mains cable

Long waterproof AC cable to microinverter

Passive cooling (no fans)

Cannot be reverse connected

---

## Internal Layout Design 

```

[ Mains AC Socket ]
     ∆
     │
     │  (Schuko plug)
     |
┌──────────────────────────┐
│   Gateway Enclosure           │
│                               │
│  AC → PSU → 5V Bus           │
│           │                   │
│     ┌────┴────┐             │
│     │ Raspberry │◄──────┐   │
│     │ Pi Zero 2 │         │   │
│     └────┬────┘         │   │
│           │ MQTT          │   │
│     ┌────┴────┐         │   │
│     │ OpenDTU │ RF ⇄ Inverter|
│     │ Fusion  │           │   │
│     └─────────┘         │   │
│     ┌────┴────┐         │   |
│     | H&T Sensor│ ________|   |
|     └────┬────┘             |
└──────────────────────────┘
      │
      │ (AC cable with connector)
      ▼
 [ Hoymiles Microinverter ]

NOTE: AC cable length limit - maximum 10 m between gateway and microinverter to minimize voltage drop and ensure reliable inverter operation.

```

---

## Raspberry Pi Software Stack


The Raspberry Pi runs a minimal, headless Linux stack designed for reliability, self-healing, and unattended operation.

**Base Operating System**
Raspberry Pi OS Lite (64-bit)
No desktop environment
Small footprint
Long-term stability
Responsibilities:
System boot and service orchestration
Persistent storage
Hardware abstraction
Network Management

**NetworkManager**
Used instead of raw wpa_supplicant.
Responsibilities:
Wi-Fi client mode (normal operation)
Temporary Wi-Fi Access Point mode (first boot)
Secure storage of credentials
Automatic recovery from network loss

First-Boot Provisioning (AP Mode)
On first boot, the Gateway Block enters temporary AP provisioning mode.
Behavior
Pi creates Wi-Fi AP:
OpenSolar-One-XXXX
User connects via phone or laptop
Captive portal opens at:
http://192.168.4.1
User enters:
Home Wi-Fi SSID
Wi-Fi password
(Optional) location or node label
Device:
Saves credentials
Reboots
Joins local router
Permanently disables AP mode
Reset
AP mode can be re-enabled via SD reflash or explicit reset flag

**Local Messaging Layer**
Mosquitto (MQTT Broker)
Runs locally on the Pi.
Responsibilities
Central message bus for all gateway devices
Receives telemetry from OpenDTU Fusion
Buffers data if WAN is unavailable
Provides stable MQTT topics regardless of internet state
Design principle
Hardware always publishes locally first.

**Solar Telemetry Ingestion**
OpenDTU Client Service
Responsibilities
Receive decoded inverter data from OpenDTU Fusion
Normalize metrics (W, Wh, voltage, current)
Publish standardized MQTT topics
Monitor inverter health and availability

**Secure Remote Connectivity**
Tailscale
Responsibilities
Encrypted outbound tunnel to central Data Block
Device identity via Tailnet
No inbound ports exposed
Auto-reconnect on network changes
Authentication
Preloaded, scoped auth key
Device auto-registers on first successful WAN connection

**Gateway Registration & Discovery**
A small service or script runs after networking is established.
Responsibilities
Detect active Tailscale connection
Announce gateway to central Home Assistant via:
MQTT registration topic or
HA webhook
Transmit:
Gateway ID
Software version
Capabilities (PV only, sensors present, etc.)
This is how the central HA instance becomes aware that a new Gateway is live.

**Reliability & Self-Healing**
Watchdog & Recovery Services
Implemented using systemd and lightweight scripts.
Responsibilities
Monitor:
Wi-Fi connectivity
MQTT broker health
Tailscale tunnel state
Restart failed services
Trigger controlled reboot if recovery fails
Goal
The Gateway must recover without user intervention.

---

## Design Summary

The Gateway Block is:

Autonomous

Headless

Secure by default

Cloud-independent

Physically minimal

Logically deterministic

It forms the input measurement foundation of OpenSolar One and can operate independently or as part of a multi-site research network.

---


## Overview

The Gateway Block is a custom, outdoor-rated integration hub designed to bridge local solar production data with remote monitoring and research infrastructure. 

It functions as a localized communication bridge for Hoymiles microinverters, converting proprietary radio telemetry into secure, internet-ready data streams while also monitoring the environmental conditions affecting the measurement hardware itself.

This block represents the energy input measurement layer of an OpenSolar One node.


---

## Hardware Architecture

**The Brain - Raspberry Pi Zero 2 W**

The Raspberry Pi Zero 2 W acts as the local server and secure gateway.

Runs a lightweight Linux OS

Hosts a local MQTT broker (Mosquitto) for ingesting telemetry

Establishes a persistent Tailscale VPN tunnel to the remote Home Assistant Green instance

Aggregates and forwards standardized solar and environmental data upstream


The Zero 2 W is selected for its:

Extremely low and predictable power draw

Sufficient CPU and network headroom for future extensions (e.g. IP camera, additional sensors)

Long-term software support and ecosystem stability

---

**The Translator - OpenDTU Fusion**

The OpenDTU Fusion is an ESP32-S3–based device running open-source firmware.

Communicates directly with the Hoymiles microinverter via Sub-1 GHz RF

Decodes proprietary inverter telemetry locally

Publishes real-time production data (W, Wh, status) over MQTT via Wi-Fi

Operates fully offline from any vendor cloud


This ensures complete data sovereignty and transparency in the energy measurement pipeline.


---

**Environmental Monitoring - Shelly H&T**

A USB-powered temperature and humidity sensor is installed inside the Gateway enclosure.

Purpose:

Monitor ambient conditions affecting the Gateway electronics

Track enclosure thermal behavior across seasons and climates

Detect overheating, condensation risk, or enclosure sealing issues

Provide standardized environmental context across all deployments


Key characteristics:

Powered directly from the Gateway’s internal 5 V supply (no batteries)

Measures enclosure air temperature and relative humidity

Data ingested via the Raspberry Pi and forwarded alongside solar telemetry

Solar availability and weather effects are inferred directly from PV power output.


---

**The Shell - Outdoor Enclosure**

The electronics are housed in a weatherproof IP65+ polycarbonate enclosure.

Features:

UV-resistant, light-colored housing for passive thermal management

Integrated 10m cable with  HMS Field Connector/BC05 Connector to connect to Hoymiles HMS microinverter range 

Integrated 1m cable with Shuko plug to connect to a standard outdoor outlet

Internal 5 V USB PSU supplying the Raspberry Pi, OpenDTU and Shelly H & T

Passive cooling with no moving parts


The enclosure is wall-mounted in a shaded exterior location to minimize direct solar heating.


---

## Internal Logic & Data Flow

**1. Capture**
   
The OpenDTU Fusion polls the Hoymiles microinverter via Sub-1 GHz RF.

The maximum supported AC cable length between inverter and panel is 10 m, ensuring minimal voltage drop and stable inverter operation.


**2. Local Relay**
   
Telemetry is transmitted over local 2.4 GHz Wi-Fi router network from the OpenDTU to the Raspberry Pi’s MQTT broker.


**3. Aggregation**

The Raspberry Pi aggregates:

Solar production metrics

Environmental sensor data

Device health signals


**4. Secure Tunneling**
   
All data is forwarded through an encrypted Tailscale tunnel to the remote Home Assistant Green instance without requiring port forwarding or local router configuration.


**5. Visualization & Storage**

Home Assistant auto-discovers the Gateway Block devices, enabling real-time dashboards, historical storage, and long-term research analysis.


---

## Installation Summary

Mounted on an exterior wall in a shaded location

Powered from 240v mains supply via the integrated socket

Entirely passively cooled

Requires only local Wi-Fi access and internet connectivity


Once installed, the Gateway Block operates autonomously and requires no routine maintenance, forming a stable and reproducible foundation for OpenSolar One deployments.

