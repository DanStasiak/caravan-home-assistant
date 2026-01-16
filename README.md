# 🚐 Caravan Home Assistant

![HACS](https://img.shields.io/badge/HACS-Custom-orange.svg)
![Home Assistant](https://img.shields.io/badge/Home%20Assistant-2024.0%2B-blue.svg)
![ESPHome](https://img.shields.io/badge/ESPHome-Supported-green.svg)

### Smart Mobile Trailer platform powered by Home Assistant  
**Reference implementation: Hobby Excellent 540 FU (2019)**

Turn a **travel trailer (caravan / Wohnwagen)** into a **fully monitored, remotely accessible, and extensible smart system** using **Home Assistant**, **ESPHome**, and open standards.

This repository is a **real, running system**, not a demo.  
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
  👉 `packages/power`

- 🌡️ **Climate & Zones**
  - Sleeping, living, kitchen, bathroom
  - Outside temperature
  - Alerting & summaries
  - Prepared for Truma Bluetooth integration  
  👉 `packages/climate`

- 💡 **Lighting**
  - Centralized logic
  - Zigbee-first approach  
  👉 `packages/lighting`

- 🚰 **Water monitoring**
  - Fresh-water tank level
  - No drilling required
  - ESPHome-based continuous percentage  
  👉 `packages/water`

- 📍 **GPS & Location**
  - Automatic GPS device_tracker detection
  - Location awareness & display  
  👉 `packages/gps`

- 📶 **Connectivity**
  - WAN monitoring
  - Starlink + LTE failover awareness
  - GL.iNet router integration  
  👉 `packages/connectivity`

- 📊 **Mobile-first dashboards**
  - Clean UI
  - Touch-friendly
  - Severity-based status model  
  👉 `dashboards`

- 🔔 **Notifications & Alerts**
  - Central notification abstraction
  - Push + optional TTS
  - Quiet hours & suppression
  - Severity-aware behavior  
  👉 `packages/alerts`

- 📐 **Leveling (travel trailer safe)**
  - Front-only leveling
  - ESPHome IMU
  - Calibration UI  
  👉 `packages/leveling`

- 🧩 **ESPHome nodes**
  - Modular ESP32 configs
  - OTA-ready
  - Reusable patterns  
  👉 `esphome`

- 🖨️ **3D-printed enclosures**
  - Custom cases for ESP & sensors  
  👉 `hardware/stl`

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

### Install via HACS
1. Open **HACS → Integrations → ⋮ → Custom repositories**
2. Add: `https://github.com/DanStasiak/caravan-home-assistant`
3. Category: **Integration**
4. Install and restart Home Assistant

---

## 🔎 Auto-discovery

- **ESPHome**: discovered automatically via mDNS / ESPHome API
- **Zigbee2MQTT**: devices appear via MQTT discovery
- **Bluetooth**: via native adapter or ESPHome Bluetooth proxy
- **Dashboards**: YAML dashboards included under `dashboards/`

---

## 🚧 Project status

- Core systems: **Production**
- Some integrations: **Lab / evolving**
- Actively developed and used in real travel

---

## ⚠️ Disclaimer

DIY project. No warranty.  
You are responsible for electrical safety, compliance, and hardware changes.

---

## 🤝 Contributing

Issues and PRs are welcome—especially improvements that make adaptation to other trailers easier.
