# 🚐 Caravan Home Assistant
### Smart Mobile Trailer platform powered by Home Assistant  
**Reference implementation: Hobby Excellent 540 FU (2019)**

Turn a **travel trailer (caravan / Wohnwagen)** into a **fully monitored, remotely accessible, and extensible smart system** using **Home Assistant**, **ESPHome**, and open standards.

This repository is a **complete solution / reference architecture**, not a Home Assistant integration or HACS component.

> ✅ Designed for **travel trailers**  
> ❌ Not intended for motorhomes  
> ❌ No 4-point leveling logic (front-only leveling)

---

## ✨ What this project is

This project documents and implements a **real, running Mobile Assistant** inside a travel trailer.

It combines:
- Home Assistant OS
- ESPHome (ESP32-based nodes)
- Zigbee (Zigbee2MQTT)
- Bluetooth (GPS, future Truma integration)
- YAML-first configuration
- Git-managed structure

The result is a **mobile-first smart caravan system** covering monitoring, control, and alerting.

---

## ✅ Implemented components (current)

### 📐 Caravan Leveling (travel-trailer safe)
Front-only leveling designed specifically for travel trailers:
- ESPHome IMU-based sensors
- Reset / set-level calibration workflow
- Dedicated mobile Lovelace view

👉 Package: `packages/caravan_leveling`

---

## 🧭 Roadmap (planned / in progress)

The following modules are part of the project vision and will be added incrementally:

- ⚡ Power & Energy (battery, SOC, charging, alerts)
- 🌡️ Climate & Zones (sleeping / living / kitchen / bathroom)
- 💡 Lighting (Zigbee-first)
- 🚰 Water monitoring (no drilling solutions)
- 📍 GPS & Location (auto-detection)
- 📶 Connectivity (Starlink + LTE failover)
- 🔔 Notifications (push + optional TTS, quiet hours)
- 📊 Mobile-first dashboards
- 🧩 ESPHome node library
- 🖨️ 3D-printed enclosures

---

## 📸 Screenshots

Screenshots will be added once the main dashboards are finalized:
- Caravan Mobile overview
- Leveling calibration
- Power & climate views

---

## 🧠 Architecture overview

Home Assistant runs **locally inside the caravan** and acts as the central brain.

Typical setup:
- Raspberry Pi 4 running Home Assistant OS
- ESP32 nodes running ESPHome
- Zigbee coordinator + Zigbee2MQTT
- Bluetooth adapters / proxies

All logic is implemented in **YAML packages**, not Python integrations.

---

## 📦 Installation (manual)

This repository is **not HACS-installable by design**.

### Installation steps

1. Clone or download the repository:
   ```bash
   git clone https://github.com/DanStasiak/caravan-home-assistant.git
   ```
2. Copy the following folders into your Home Assistant `/config` directory:
   - `packages/`
   - `dashboards/`
   - `templates/`
   - `scripts/`
   - `esphome/`
   - `hardware/`
   - `docs/`
3. Restart Home Assistant

---

## ⚙️ Required Home Assistant configuration

Enable packages in `configuration.yaml`:

```yaml
homeassistant:
  packages: !include_dir_merge_named packages
```

---

## 🔎 Auto-discovery behavior

- **ESPHome** devices are discovered automatically via mDNS / native API
- **Zigbee2MQTT** devices appear via MQTT discovery
- **Bluetooth** devices appear via native adapters or ESPHome Bluetooth proxies
- **Dashboards** are provided as YAML and can be imported manually

---

## 🔧 Adapting to other caravans

Reusable across most travel trailers:
- dashboards
- alert & notification logic
- connectivity monitoring
- ESPHome patterns

Trailer-specific adjustments:
- lighting zones
- water tank wiring
- sensor placement
- entity naming

The **Hobby Excellent 540 FU** is the reference, not a limitation.

---

## 🚧 Project status

- Leveling module: **Production**
- Other modules: **Roadmap / active development**

---

## ⚠️ Disclaimer

DIY project. No warranty.

You are responsible for:
- Electrical safety
- Regulatory compliance
- Hardware modifications

---

## 🤝 Contributing

Issues, discussions, and pull requests are welcome — especially improvements that make the system easier to adapt to other travel trailers.
