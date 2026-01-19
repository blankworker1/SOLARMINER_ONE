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

Mounting	Balcony / rail mounting system	Must meet local safety codes



---

### 2.2 Grid Interface

Component	Reference	Notes

Micro‑Inverter:	Hoymiles HMS‑800W‑2T	

Balcony PV compliant, dual MPPT (not W model)

Inverter Gateway:	OpenDTU Fusion

Local monitoring & control

AC Connection:	Standard mains outlet


Communication path:

HMS‑800W‑2T → OpenDTU Fusion via Sub‑1 GHz RF (over‑the‑air)

OpenDTU Fusion → Local network via Wi‑Fi (2.4 GHz only)

Home Assistant connects to OpenDTU via local router network


This architecture enables full local monitoring and control without reliance on the Hoymiles cloud.

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

- Local control plane

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

### 2.6 Cooling

Component	Reference	Notes

Fan	5 V USB fan	Low‑RPM, continuous rated

Fan Switch	Wi‑Fi USB switch	Software‑controlled


Fan behavior:

Triggered via Bitaxe internal temperature

Controlled by Home Assistant logic



---

### 2.7 Enclosure

Component	Reference	Notes

Enclosure	Desktop enclosure	Ventilated, grounded


Requirements:

Adequate airflow

Electrical grounding

Internal mounting for PSUs

LAN port access



---

## 3. Optional Research Instrumentation

These components are not required for normal operation but may be deployed for research studies.

### 3.1 Environmental Sensing

Component	Reference	Notes

Temperature Sensor:	Shelly H&T (Wi‑Fi)	Outdoor‑rated enclosure required


Placement guidelines:

Mounted behind the PV panel

Measures panel‑adjacent air temperature

Not in direct contact with panel surface

Not exposed to direct sunlight


Collected data is not shown on the user dashboard.


---

## 4. Networking Requirements

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

## 5. Power Architecture (Reference)

All devices powered via manufacturer‑supplied adapters

No shared internal DC bus in reference implementation

Grid provides stability and smooth startup/shutdown


Future revisions may define a consolidated power architecture.


---

## 6. Substitutions and Variants

To maintain data comparability:

Core components must not be substituted without documentation

Optional instrumentation may vary

All deviations must be recorded in node metadata



---

## 7. Compliance Notes

Users are responsible for local electrical compliance

Balcony PV legality varies by country

This project provides no legal certification



---

## 8. Bill of Materials Summary

Core Node (excluding PV panel):

Bitaxe NerdQAxe+

Home Assistant Green

OpenDTU Fusion

2 x Shelly Plug Gen3

USB fan + Wi‑Fi switch

Desktop enclosure


Optional:

Shelly H&T temperature sensor



---

## 9. Revision History

v0.1 – Initial reference hardware definition











