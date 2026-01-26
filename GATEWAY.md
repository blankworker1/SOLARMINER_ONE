# GATEWAY BLOCK


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

The Gateway electronics are housed in a weatherproof IP65+ polycarbonate enclosure.

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

