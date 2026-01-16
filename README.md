# 🚐 Caravan Home Assistant

[![HACS](https://img.shields.io/badge/HACS-Custom-orange.svg)](https://hacs.xyz/)
[![Home Assistant](https://img.shields.io/badge/Home%20Assistant-2024.0%2B-blue.svg)](https://www.home-assistant.io/)
[![ESPHome](https://img.shields.io/badge/ESPHome-Supported-green.svg)](https://esphome.io/)
[![License](https://img.shields.io/github/license/DanStasiak/caravan-home-assistant)](LICENSE)
[![Last Commit](https://img.shields.io/github/last-commit/DanStasiak/caravan-home-assistant)](https://github.com/DanStasiak/caravan-home-assistant/commits/main)

### Smart Mobile Trailer platform powered by Home Assistant  
**Reference implementation: Hobby Excellent 540 FU (2019)**

Turn a **travel trailer (caravan / Wohnwagen)** into a **fully monitored, remotely accessible, and extensible smart system** using **Home Assistant**, **ESPHome**, and open standards.

This repository represents a **real, running system**, not a demo or concept.  
It is designed to be **easily adapted** to other travel trailers by adjusting hardware mappings and entity names.

> ✅ Designed for **travel trailers**  
> ❌ Not intended for motorhomes  
> ❌ No 4-point leveling logic (front-only leveling)

---

## ✨ What this project delivers

- ⚡ **Power & Energy**
  - Battery voltage, current, SOC
  - Charging & power availability
  - Alerts and thresholds
  - Prepared for AGM → LiFePO₄ upgrades

- 🌡️ **Climate & Zones**
  - Sleeping, living, kitchen, bathroom
  - Outside temperature
  - Alerting & summaries
  - Prepared for Truma Bluetooth integration

- 💡 **Lighting**
  - Centralized logic
  - Zigbee-first approach

- 🚰 **Water monitoring**
  - Fresh-water tank level
  - No drilling required
  - ESPHome-based continuous percentage

- 📍 **GPS & Location**
  - Automatic GPS device_tracker detection
  - Location awareness & display

- 📶 **Connectivity**
  - WAN monitoring
  - Starlink + LTE failover awareness
  - GL.iNet router integration

- 📊 **Mobile-first dashboards**
  - Clean UI
  - Touch-friendly
  - Severity-based status model

- 🔔 **Notifications & Alerts**
  - Central notification abstraction
  - Push + optional TTS
  - Quiet hours & suppression
  - Severity-aware behavior

- 📐 **Leveling (travel trailer safe)**
  - Front-only leveling
  - ESPHome IMU
  - Calibration UI

- 🧩 **ESPHome nodes**
  - Modular ESP32 configs
  - OTA-ready
  - Reusable patterns

- 🖨️ **3D-printed enclosures**
  - Custom cases for ESP & sensors

---

## 📸 Screenshots

> Screenshots will be added soon:
> - Caravan Mobile dashboard
> - Power overview
> - Climate zones
> - Connectivity status
> - Leveling calibration

---

## 🧠 Architecture overview

Home Assistant runs **locally inside the caravan** and acts as the central brain.

- Home Assistant OS (Raspberry Pi 4)
- ESPHome (ESP32 sensors & actuators)
- Zigbee (via Zigbee2MQTT)
- Bluetooth (GPS, future Truma integration)
- YAML-first, Git-managed configuration

---

## 📦 Installation (HACS-ready)

This repository is a **package-style Home Assistant project**.  
HACS is used as a **distribution & update mechanism**.

### Install via HACS (recommended)

1. Open **HACS → Integrations → ⋮ → Custom repositories**
2. Add:  
   ```
   https://github.com/DanStasiak/caravan-home-assistant
   ```
3. Category: **Integration**
4. Install and restart Home Assistant

---

## 🔎 Auto-discovery

- **ESPHome**: discovered automatically via mDNS / ESPHome API
- **Zigbee2MQTT**: devices appear via MQTT discovery
- **Bluetooth**: via native adapter or ESPHome Bluetooth proxy
- **Dashboards**: YAML dashboards included under `dashboards/`

---

## 🔧 Adapting to other caravans

Reusable as-is:
- dashboards
- notification & alert framework
- connectivity logic
- ESPHome patterns

Trailer-specific adjustments:
- lighting zones
- water tank wiring
- sensor placement
- entity naming

---

## 🚧 Project status

- Core systems: **Production**
- Some integrations: **Lab / evolving**
- Actively developed and used during real travel

---

## ⚠️ Disclaimer

DIY project. No warranty.  
You are responsible for electrical safety, regulatory compliance, and hardware changes.

---

## 🤝 Contributing

Issues and pull requests are welcome—especially improvements that make adaptation to other caravans easier.
