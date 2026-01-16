# 🚐 Caravan Home Assistant  
### A Smart Mobile Trailer Platform powered by Home Assistant

This project turns a **travel trailer (caravan)** into a **fully monitored, remotely accessible, and extensible smart system** using **Home Assistant**, **ESPHome**, and open standards.

The reference implementation is based on a **Hobby Excellent 540 FU**, but the architecture is **intentionally modular** and can be adapted to **most travel trailers** with minimal changes.

> ⚠️ This project is designed for **travel trailers (Wohnwagen)**  
> ❌ Not intended for motorhomes  
> ❌ No 4-point leveling logic

---

## ✨ Project Goals

- Create a **Mobile Assistant** for caravans
- Monitor and control **as much as possible**, including:
  - Power & battery
  - Climate & heating
  - Lighting
  - Water levels
  - Connectivity & GPS
- Provide a **mobile-first UI** for on-site and remote access
- Use **open, vendor-neutral technologies**
- Be **reproducible, documented, and version-controlled**

This is **not a single dashboard**, but a **complete system architecture**.

---

## 🏕️ Reference Trailer

- **Model:** Hobby Excellent 540 FU
- **Year:** 2019
- **Why Hobby?**
  - Very common in Europe
  - Well-documented electrical layout
  - Good candidate for non-destructive upgrades

All Hobby-specific logic is **clearly separated** so other trailers can reuse the core system.

---

## 🧠 System Architecture Overview

Home Assistant OS runs locally inside the caravan and acts as the central brain.  
ESPHome nodes, Zigbee devices, and Bluetooth integrations provide distributed sensing and control.

Core technologies:
- Home Assistant OS
- ESPHome (ESP32 based)
- Zigbee (Zigbee2MQTT)
- Bluetooth (passive + proxy)
- YAML-first configuration
- GitHub-managed

---

## ⚡ Power & Energy Monitoring

Implemented and documented:
- Battery voltage, current, SOC
- Charging state
- Power availability
- Prepared for AGM → LiFePO₄ migration
- Alerting on critical states

Related components:
- packages/power/
- templates/power.yaml
- dashboards/caravan-power.yaml

---

## 🌡️ Climate & Environment

- Multiple temperature zones (sleeping, living, kitchen, bathroom)
- Outside temperature
- Prepared for Truma heating integration (Bluetooth)
- Alerting for abnormal conditions

Related components:
- packages/climate/
- templates/zones.yaml
- dashboards/caravan-climate.yaml

---

## 💡 Lighting Control

- Centralized lighting logic
- Zigbee-based
- Easily expandable per trailer layout

Related components:
- packages/lighting/

---

## 🚰 Water Monitoring

- Fresh water tank monitoring
- No drilling required
- ESPHome-based
- Continuous percentage calculation
- Compatible with multi-probe tanks

Related components:
- packages/water/
- esphome/water-tank.yaml

---

## 📍 GPS & Connectivity

- Automatic GPS device detection
- Location tracking
- WAN monitoring
- Starlink + LTE failover awareness
- GL.iNet router integration

Related components:
- packages/connectivity/
- packages/gps/
- scripts/router_status.py

---

## 📊 Dashboards & UX

Designed mobile-first but usable on desktop.

Key views:
- Caravan overview
- Power
- Climate
- Connectivity
- Leveling
- Maintenance

Design principles:
- OK / Attention / Alarm severity model
- Mushroom UI components
- Touch-friendly layout

Dashboards:
- dashboards/caravan-mobile.yaml
- dashboards/caravan-home.yaml

---

## 📐 Leveling System (Travel Trailer)

- Front-only leveling
- ESPHome IMU-based
- Calibration UI included
- Designed specifically for travel trailers

Related components:
- packages/leveling/
- esphome/imu-level.yaml
- dashboards/caravan-level.yaml

---

## 🧩 ESPHome Nodes

- Modular ESP32 nodes
- OTA-ready
- YAML included
- Custom 3D-printed enclosures supported

Configs:
- esphome/

STL files:
- hardware/stl/

---

## 🔔 Notifications & Alerts

Centralized notification system:
- Push notifications
- Optional TTS
- Quiet hours
- Alert suppression
- Severity-based behavior

Implementation:
- scripts/caravan_notify.yaml
- packages/alerts/

---

## 📦 Repository Structure

caravan-home-assistant/
├── dashboards/
├── packages/
├── templates/
├── scripts/
├── esphome/
├── hardware/
│   └── stl/
├── docs/
└── README.md

---

## 🔌 Hardware Used (Reference)

- Raspberry Pi 4 (Home Assistant OS)
- ESP32 dev boards
- Temperature & humidity sensors
- IMU (leveling)
- Zigbee coordinator
- GL.iNet router
- Optional Starlink

Exact models are documented in docs/hardware.md.

---

## 🧰 Prerequisites

- Home Assistant OS (recent version)
- ESPHome
- Zigbee2MQTT
- HACS (recommended)
- Basic YAML knowledge

This is a DIY-oriented project.

---

## 🔄 Adapting to Other Caravans

Reusable:
- Dashboards
- ESPHome nodes
- Alerts
- Connectivity logic

Trailer-specific:
- Water tank wiring
- Lighting zones
- Physical layout

---

## 🚧 Project Status

- Core systems: Production
- Some integrations: Lab
- Actively developed

---

## 📄 License & Disclaimer

Provided as-is, without warranty.

You are responsible for:
- Electrical safety
- Compliance with regulations
- Hardware modifications

---

## 🤝 Contributions

Issues and improvements are welcome.
