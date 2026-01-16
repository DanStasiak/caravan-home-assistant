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

## ✅ Implemented (in this repository)

### 📐 Caravan Leveling (travel-trailer safe)
Front-only leveling package for travel trailers:
- IMU-based sensors (ESPHome)
- Reset / set-level calibration flow
- Mobile-first Lovelace view

👉 **Package:** [`packages/caravan_leveling`](packages/caravan_leveling)

---

## 🧭 Roadmap (planned / in progress)

These are core goals of the project and will be added as packages/modules:
- ⚡ Power & Energy (battery, SOC, charging, alerts)
- 🌡️ Climate & zones (sleeping/living/kitchen/bathroom + outside)
- 💡 Lighting (Zigbee-first)
- 🚰 Water monitoring (no drilling)
- 📍 GPS & location (auto-detect tracker)
- 📶 Connectivity (Starlink + LTE + router state)
- 🔔 Notifications framework (push + optional TTS, quiet hours, suppression)
- 📊 Mobile-first dashboards for each subsystem
- 🧩 ESPHome node library + 3D-printable enclosures

---

## 📸 Screenshots
Screenshots will be added soon:
- Caravan Mobile dashboard
- Leveling calibration view

---

## 🧠 Architecture overview

Home Assistant runs **locally inside the caravan** and acts as the central brain.

- Home Assistant OS (Raspberry Pi 4)
- ESPHome (ESP32 sensors & actuators)
- Zigbee (via Zigbee2MQTT)
- Bluetooth (GPS, future Truma integration)
- YAML-first, Git-managed configuration

---

## 🗂️ File layout

Expected Home Assistant structure:

```
/config
  /packages
  /dashboards
  /templates
  /scripts
  /esphome
  /hardware
  /docs
```

This repo mirrors that layout intentionally.

---

## ⚙️ Required Home Assistant configuration

Enable packages in `configuration.yaml`:

```yaml
homeassistant:
  packages: !include_dir_merge_named packages
```

---

## 🔎 Auto-discovery

- **ESPHome**: discovered automatically via mDNS / ESPHome API
- **Zigbee2MQTT**: devices appear via MQTT discovery
- **Bluetooth**: via native adapter or ESPHome Bluetooth proxy
- **Dashboards**: YAML dashboards will be included under `dashboards/`

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

## 🧾 Repo “About” settings (recommended for HACS listing quality)

In GitHub, open your repo and use the **right sidebar “About”** box:

- **Description (suggested):**  
  *Smart Mobile Trailer platform for Home Assistant (Hobby Excellent 540 FU reference)*
- **Topics (suggested):**  
  `home-assistant`, `hacs`, `esphome`, `caravan`, `wohnwagen`, `travel-trailer`, `hobby`, `iot`, `zigbee`, `mqtt`

---

## 🚧 Project status

- Leveling: **Production**
- Other modules: **Roadmap / in progress**
- Actively developed and used during real travel

---

## ⚠️ Disclaimer

DIY project. No warranty.  
You are responsible for electrical safety, regulatory compliance, and hardware changes.

---

## 🤝 Contributing

Issues and pull requests are welcome—especially improvements that make adaptation to other caravans easier.
