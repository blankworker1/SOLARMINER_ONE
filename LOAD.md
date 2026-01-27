# LOAD BLOCK 

![OS1 Block Diagram](https://emerald-real-clownfish-172.mypinata.cloud/ipfs/bafkreihxirlx2eo6epbrn3o4qoeo327bkg7ucczh6h6k5dkgpp6zlddw6y)

## Overview

The Load Block performs a deterministic computational workload and provides precise measurement of the electrical energy required to produce that work. Within the OpenSolar One platform, it represents the output side of the solar-to-computation measurement chain.

The Load Block is electrically and logically autonomous. This separation ensures clean attribution of energy consumption, reproducible results across sites, and safe operation independent of solar generation hardware.

Bitcoin mining is used solely as a measurement mechanism: a globally verifiable, deterministic way to account for computational work.


---

## Functional Role

The Load Block answers one core research question:

> How much verifiable computational work is produced per unit of electrical energy?



It provides:

A standardized computational workload

High-resolution energy measurement

Transparent operational control

Verifiable, auditable output metrics



---

## Hardware Architecture

Core Components

**Bitaxe-class Miner (e.g. NerdQAxe+)**

Standardized computational workload

Runs open firmware (AxeOS)

Exposes telemetry via local API (hashrate, temperature, uptime)


**Isolated Power Supply Unit (PSU)**

Dedicated AC→DC supply for the miner

Electrically isolated from other system blocks

Ensures stable and repeatable power delivery


**Shelly Plug Gen3**

Inline smart power meter between mains and PSU

Measures real-time and cumulative energy usage (W, Wh)

Enables remote hard power-cycling


---

## Electrical Characteristics

Component	Typical Power	Notes

Bitaxe Miner	~90 W	Configurable via firmware

PSU Efficiency	≥85%	Losses included via AC-side measurement

Shelly Plug Gen3	<2 W	Negligible measurement impact


All energy measurements are taken at the AC input to the Load Block, ensuring that PSU losses are fully accounted for.


---

## Connectivity

Miner → Local Router

Wi-Fi (2.4 GHz)

Used for telemetry and configuration via AxeOS API


Shelly Plug → Local Router

Wi-Fi (2.4 GHz)

Provides power telemetry and remote switching


No Direct Dependency on Gateway Block

The Load Block operates independently

Data is aggregated centrally by the Data Block (Home Assistant Green)




---

## Configuration & Provisioning (User Steps)

Provisioning is a one-time local process. The user only connects devices to their home Wi-Fi. No Home Assistant access or cloud accounts are required.

**Bitaxe Miner Provisioning**

1. Power on the miner


2. Miner boots into Wi-Fi AP mode
(SSID e.g. Bitaxe-XXXX)


3. User connects phone/laptop to the miner AP


4. Open browser at:

http://192.168.4.1


5. Enter:

Home Wi-Fi SSID

Wi-Fi password

Mining pool credentials

Wallet lightning payment URL (check braiins API)


6. Miner saves settings, reboots, and joins the local router
AP mode disables automatically



**Shelly Plug Gen3 Provisioning**

1. Plug in the Shelly Plug


2. Shelly starts in AP mode
(SSID e.g. ShellyPlug-XXXX)


3. User connects to the Shelly AP


4. Open browser at:

http://192.168.33.1


5. Enter:

Home Wi-Fi SSID

Wi-Fi password



6. Shelly joins the local router
AP mode disables automatically



⚠️ Shelly Cloud is not required and should remain disabled.


---

## Data Outputs

**Energy Metrics**

Instantaneous power draw (W)

Cumulative energy consumption (Wh, kWh)

Uptime and downtime periods


**Computation Metrics**

Hashrate (H/s)

Accepted work units

Miner temperature

Error and fault states


All metrics are timestamped and forwarded to the Data Block (Home Assistant Green) for correlation with solar input data.


---

## Control & Automation

The Load Block supports non-intrusive remote management via Home Assistant:

Automated power-cycling using the Shelly Plug

Conditional restart if:

Hashrate drops to zero

Thermal thresholds are exceeded


Manual intervention is rarely required



---

## Design Principles

Isolation – clean separation from solar input

Transparency – open firmware and measurable interfaces

Reproducibility – identical hardware across deployments

Fail-safe recovery – hard reset without physical access



---

## Summary

The Load Block is a self-contained, reproducible unit that converts electrical energy into verifiable computational work and precisely measures the cost of that conversion. When combined with the Gateway Block’s solar measurements, it enables rigorous analysis of solar-powered computation across locations, seasons, and climates.

The Load Block specification is stable for OpenSolar One v1 and must remain unchanged across research deployments to preserve dataset integrity.





