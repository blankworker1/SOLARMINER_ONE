# HARDWARE

## SolarMiner One – Hardware Reference List

This document defines the reference hardware specification for a SolarMiner One node.

The goal is to ensure that all deployments use identical, reproducible, off‑the‑shelf components, enabling direct comparison of data across sites and long time periods.

All listed components are commercially available and may be substituted only where explicitly noted.


---

## 1. Design Principles

- Use only off‑the‑shelf hardware

- Avoid proprietary lock‑in

- Prefer devices with local APIs and Home Assistant support

- Minimize moving parts and maintenance

- Maintain regulatory compatibility across EU jurisdictions

- Separate core system from optional research instrumentation



---

## 2. Core System Hardware

These components define a valid SolarMiner One reference node.

### 2.1 Solar Generation

Component	Reference	Notes

PV Panel	400–500 W monocrystalline panel	Balcony‑scale, user supplied

Mounting	Balcony / rail mounting system	- to meet local safety codes



---

### 2.2 Grid Interface

Component	Reference	Notes

Micro‑Inverter:	Hoymiles HMS‑800W‑2T	- Balcony PV compliant, dual MPPT (not W model), AC mains using manufacturers HMS Field Connector connected to Gateway Block cable

Inverter Gateway:	OpenDTU Fusion - for local data transfer 



Communication path:

HMS‑800W‑2T → OpenDTU Fusion via Sub‑1 GHz RF (over‑the‑air)

OpenDTU Fusion → Local network via Wi‑Fi (2.4 GHz only)

Raspberry Pi MQTT from local network via Wi-Fi 

Raspberry Pi to remote Home Assistant Green


This architecture enables monitoring and control without reliance on the Hoymiles cloud.

---

### 2.3 Computation

Component	Reference	Notes

Compute Device	Bitaxe NerdQAxe+	

~90 W, Wi‑Fi connected

Power Supply	Manufacturer‑supplied PSU	240 V AC → 12 V DC


The Bitaxe provides:

Deterministic workload

On‑device temperature telemetry

Network‑accessible API



---

### 2.4 System Controller

Component	Reference	Notes

Controller:	Home Assistant Green	

Headless operation

Network: 	Ethernet (LAN)	Local router required

Power Supply: 	Manufacturer‑supplied PSU	240 V AC → 12 V DC


Home Assistant Green acts as:

- Remote control plane

- Data collection hub

- Long‑term logger



---

### 2.5 Power Monitoring

Component	Reference	Notes

Smart Plug A	Shelly Plug Gen3	PV output monitoring (back up)

Smart Plug B	Shelly Plug Gen3	System power monitoring


Characteristics:

Wi‑Fi connectivity

Local API

Bidirectional power measurement


---

### 2.6 Environmental Sensing

Component	Reference	Notes

Temperature Sensor:	Shelly H&T wifi humidity and temperature sensor 


Placement guidelines:

Mounted in Gateway Block enclosure 

Collected data is not shown on the user dashboard.


---

## 3. Networking Requirements

Local Wi‑Fi network (2.4 GHz required) for:

OpenDTU Fusion

Bitaxe miner

Shelly smart plugs

Optional sensors


Wired Ethernet connection for Home Assistant Green

Internet access for:

Time synchronization

Remote data streaming (research deployments)



No vendor cloud services are required for operation.


---

## 4. Power Architecture (Reference)

Gateway Block enclosure - all devices powered via shared internal DC adapter

Load Block - powered by manufacturer supplied adapter

Data Block - powered by manufacture supplied adapter 

Grid provides stability and smooth startup/shutdown

Future revisions may define a consolidated power architecture.


---

## 5. Substitutions and Variants

To maintain data comparability:

Core components must not be substituted without documentation

Optional instrumentation may vary

All deviations must be recorded in node metadata



---

## 6. Compliance Notes

Users are responsible for local electrical compliance

Balcony PV legality varies by country

This project provides no legal certification



---

## 7. Bill of Materials Summary


**Gateway Block (excluding PV panels + microinverter):**

Raspberry Pi Zero 2 W + SD card 

OpenDTU Fusion

Shelly H&T humidity and temperature sensor

240v to 5v USB PSU

Shelly Plug Gen3 (backup monitoring)

Waterproof enclosure


**Load Block:**

NerdQAxe+ 

Shelly Plug Gen3


**Data Block:**

Home Assistant Green + PSU 


---

## 8. Revision History

v0.1 – Initial reference hardware definition











