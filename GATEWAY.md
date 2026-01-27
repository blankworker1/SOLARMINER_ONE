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

**Power Supply** - 240v mains to 5vdc, two USB ports, high-quality, isolated PSU powering:

Raspberry Pi Zero 2 W

OpenDTU Fusion

USB-powered sensors

---

**Weatherproof Enclosure** - configured as an inline adapter module with:

Short Schuko AC mains cable

Long waterproof AC cable to microinverter

UV-resistant, light-colored housing for passive thermal management (no fans)

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

```

NOTE: Integrated AC cable with HMS Field Connector/BC05 Connector to connect to Hoymiles HMS microinverter range. 

Maximum 10 m between gateway and microinverter to minimize voltage drop and ensure reliable inverter operation.

---

## Internal Logic & Data Flow

**1. Capture**
   
The OpenDTU Fusion polls the Hoymiles microinverter via Sub-1 GHz RF.


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

## Raspberry Pi Software Stack


The Raspberry Pi runs a minimal, headless Linux stack designed for reliability, self-healing, and unattended operation.

**Base Operating System**

Raspberry Pi OS Lite (64-bit)

No desktop environment, Small footprint, Long-term stability

Responsibilities: System boot and service orchestration,Persistent storage, Hardware abstraction


**Network Management**


NetworkManager - Used instead of raw wpa_supplicant.

Responsibilities: Wi-Fi client mode (normal operation), Temporary Wi-Fi Access Point mode (first boot), Secure storage of credentials, Automatic recovery from network loss



**First-Boot Provisioning (AP Mode)**

On first boot, the Gateway Block enters temporary AP provisioning mode.

Behavior: 

- Pi creates Wi-Fi AP: OpenSolar-One-XXXX, 
- User connects via phone or laptop
- Captive portal opens at: http://192.168.4.1
- User enters: Home Wi-Fi SSID, Wi-Fi password, location or node label
- Pi saves credentials, reboots, joins local router, permanently disables AP mode

NOTE: Reset AP mode can be re-enabled via SD reflash



**Local Messaging Layer**

Mosquitto (MQTT Broker) runs locally on the Pi.

Responsibilities: central message bus for all gateway devices, receives telemetry from OpenDTU Fusion, buffers data if WAN is unavailable, provides stable MQTT topics regardless of internet state.

NOTE: Design principle - hardware always publishes locally first.



**Solar Telemetry Ingestion**

OpenDTU Client Service

Responsibilities: receive decoded inverter data from OpenDTU Fusion, normalize metrics (W, Wh, voltage, current), publish standardized MQTT topics, monitor inverter health and availability.




**Secure Remote Connectivity**

Tailscale

Responsibilities: encrypted outbound tunnel to central Data Block, device identity via Tailnet, no inbound ports exposed, auto-reconnect on network changes

Authentication: preloaded, scoped auth key

Device auto-registers on first successful WAN connection



**Gateway Registration & Discovery**

A small service or script runs after networking is established.

Responsibilities: detect active Tailscale connection, announce gateway to central Home Assistant via MQTT registration topic or HA webhook

Transmit: Gateway ID, Software version, Capabilities (PV only, sensors present, etc.)

This is how the central HA instance becomes aware that a new Gateway is live.



**Reliability & Self-Healing**

Watchdog & Recovery Services - implemented using systemd and lightweight scripts.

Responsibilities: Restart failed services, Trigger controlled reboot if recovery fails.

Monitor: Wi-Fi connectivity, MQTT broker health, Tailscale tunnel state

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

It forms the input measurement foundation of OpenSolar One and every OpenSolar One can operate independently or as part of a multi-site research network.






