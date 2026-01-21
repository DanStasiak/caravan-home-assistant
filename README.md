[![Buy Me a Coffee](https://img.shields.io/badge/Buy%20Me%20a%20Coffee-support-yellow?logo=buy-me-a-coffee)](https://buymeacoffee.com/dstasiak)
[![Home Assistant](https://img.shields.io/badge/Home%20Assistant-YAML--first-blue?logo=home-assistant)](https://www.home-assistant.io/)
[![ESPHome](https://img.shields.io/badge/ESPHome-supported-green?logo=esphome)](https://esphome.io/)
[![YAML](https://img.shields.io/badge/Config-YAML--only-informational)](https://yaml.org/)


# 🚐 Caravan Home Assistant
### Smart Mobile Trailer platform powered by Home Assistant  
**Reference implementation: Hobby Excellent 540 FU (2019)**

Turn a **travel trailer (caravan / Wohnwagen)** into a **fully monitored, remotely accessible, and extensible smart system** using **Home Assistant**, **ESPHome**, and open standards.

This repository is a **complete solution / reference architecture**, not a Home Assistant integration or HACS component.  
It documents a **real, running system**, built incrementally and used in practice.

> ✅ Designed for **travel trailers**  
> ❌ Not intended for motorhomes  
> ❌ No 4‑point leveling logic (front‑only leveling)

---

## ✨ Project philosophy

This project follows a few clear principles:

- **System, not gadget** – this is a complete caravan automation stack
- **Mobile‑first UX** – dashboards optimized for phones & tablets
- **YAML‑first** – no click‑ops, everything version‑controlled
- **Vendor‑neutral** – ESPHome, Zigbee, MQTT, Bluetooth
- **Safe by design** – no unsafe automation (especially leveling)
- **Adaptable** – Hobby is the reference, not a hard requirement

---

## 🧠 Architecture overview

Home Assistant runs **locally inside the caravan** and acts as the central brain.

Typical setup:
- Raspberry Pi 4 running Home Assistant OS
- ESP32 nodes running ESPHome
- Zigbee coordinator + Zigbee2MQTT
- Bluetooth adapters / ESPHome BT proxies
- Local LAN with optional remote access

All logic is implemented using **Home Assistant packages**, templates, scripts, and dashboards –  
**no custom Python integration required**.

---

## 🧩 Implemented & planned subsystems

### 📐 Leveling (travel‑trailer safe) — *implemented*
Front‑only leveling designed specifically for travel trailers:
- ESPHome IMU‑based sensors
- Set‑level & reset calibration workflow
- Dedicated Lovelace UI
- Manual guidance only (no actuator automation)

📁 Package: `packages/caravan_leveling`

---

### ⚡ Power & Energy — *in progress*
Power monitoring and alerting focused on off‑grid usage:
- Battery voltage, current, SOC
- Charging state awareness
- Threshold‑based alerts
- Prepared for AGM → LiFePO₄ upgrades
- Designed to integrate chargers, DC‑DC, solar later

---

### 🌡️ Climate & Zones — *in progress*
Comfort and safety monitoring:
- Multiple interior zones (sleeping, living, kitchen, bathroom)
- Outside temperature
- Trend‑based alerts (too cold / too hot)
- Prepared for Truma heater integration (Bluetooth path)

---

### 💡 Lighting — *planned*
Centralized lighting control:
- Zigbee‑first approach
- Grouped by zones
- Manual override always possible
- Easily adaptable to different caravan layouts

---

### 🚰 Water monitoring — *planned*
Fresh‑water tank level monitoring:
- No drilling solutions preferred
- ESPHome‑based
- Continuous percentage calculation
- Works with common multi‑probe tanks

---

### 📍 GPS & Location — *planned*
Location awareness for a mobile system:
- Automatic GPS device detection
- Location display & status
- Foundation for geofencing & travel modes

---

### 📶 Connectivity — *planned*
Connectivity visibility and diagnostics:
- WAN status monitoring
- Starlink + LTE failover awareness
- Router state integration (GL.iNet)
- Clear “online / degraded / offline” states

---

### 🔔 Notifications & Alerts — *planned*
Central notification framework:
- Push notifications
- Optional TTS
- Quiet hours
- Suppression / maintenance mode
- Severity‑based behavior

---

### 📊 Dashboards & UX — *ongoing*
Mobile‑first dashboards:
- Caravan overview
- Power
- Climate
- Connectivity
- Leveling
- Maintenance / diagnostics

UX follows a simple severity model:
- 🟢 OK
- 🟧 Attention
- 🔴 Alarm

---

### 🧩 ESPHome node library — *ongoing*
Reusable ESPHome patterns:
- Modular ESP32 nodes
- OTA‑ready
- Clean entity naming
- Designed for reuse across caravans

---

### 🖨️ 3D‑printed enclosures — *ongoing*
Custom enclosures for ESP & sensors:
- STL files included
- Designed for caravan environment
- Easy mounting & service access

📁 Folder: `hardware/`

---

## Mobile Start Page (Caravan – Mobile)

The **Caravan (Mobile)** start page is the primary operational dashboard when traveling.
It is designed to be **mobile-first**, **high-contrast**, and **easy to read**, especially on phones.

<a href="docs/images/mobile-dashboard-home.jpg">
  <img src="docs/images/mobile-dashboard-home.jpg" width="25%" alt="Caravan Mobile Start Page" />
</a>


### What this page shows at a glance

- **Fresh Water** – current tank level with trend indication
- **Battery** – state of charge with early warning visibility
- **Temperature** – current interior temperature
- **Connectivity** – active WAN (e.g. Starlink / LTE)
- **GPS** – positioning status
- **Heating** – Truma / heating integration (experimental / lab)
- **Security** – doors, windows, alarm state
- **Level** – caravan leveling status with quick access to calibration

Each tile links to a **dedicated sub-page** for deeper diagnostics and control.


---

## 📦 Installation (manual)

This repository is **not HACS‑installable by design**.  
It is intended to be **cloned or copied** into an existing Home Assistant setup.

### Installation steps

1. Clone or download the repository:
   ```bash
   git clone https://github.com/DanStasiak/caravan-home-assistant.git
   ```
2. Copy the relevant folders into your Home Assistant `/config` directory:
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

## 🔎 Auto‑discovery behavior

- **ESPHome** devices are discovered automatically via mDNS / native API
- **Zigbee2MQTT** devices appear via MQTT discovery
- **Bluetooth** devices appear via native adapters or ESPHome BT proxies
- **Dashboards** are provided as YAML and can be imported or included manually

---

## 🔧 Adapting to other caravans

Reusable across most travel trailers:
- Dashboards
- Notification & alert logic
- Connectivity monitoring
- ESPHome patterns

Trailer‑specific adjustments:
- Lighting zones
- Water tank wiring
- Sensor placement
- Entity naming conventions

The **Hobby Excellent 540 FU** is the reference, not a limitation.

---

## 🚧 Project status


- Leveling: **Production**
- Other subsystems: **Active development**
- Used during real travel and continuously refined

---

## ⚠️ Disclaimer

This is a DIY project.

You are responsible for:
- Electrical safety
- Regulatory compliance
- Hardware modifications

Provided **as‑is**, without warranty.

---

## 🤝 Contributing
This repository is structured with **clarity, documentation, and reuse** in mind, to allow future community use and potential HACS-style distribution of individual packages.


Issues, discussions, and pull requests are welcome —  
especially improvements that make the system easier to adapt to other travel trailers.
---

## ☕ Support the project

This project is developed, tested, and maintained in real-world use, entirely in my spare time.

If this repository helps you build, learn, or improve your own **Caravan / Travel Trailer Home Assistant setup**,  
I would greatly appreciate your support by buying me a coffee.

👉 **Buy me a coffee:**  
https://buymeacoffee.com/dstasiak

Your support helps fund hardware, sensors, test setups, and ongoing development — and is very much appreciated.

Thank you!
---

## 🌍 Community & Support

This project is developed, tested, and maintained in real-world use, entirely in my spare time.

If this repository helps you build, learn, or improve your own **Caravan / Travel Trailer Home Assistant setup**,  
I would greatly appreciate your support by buying me a coffee.

👉 **Buy me a coffee:**  
https://buymeacoffee.com/dstasiak

Support helps fund hardware, sensors, test setups, documentation, and ongoing development.

Community contributions are welcome via:
- Issues for questions or discussion
- Pull requests for improvements and extensions
- Documentation enhancements for broader caravan compatibility
---

## 📦 Future HACS‑eligible packages

While this repository is currently a **full reference implementation**, parts of it are intentionally structured
to allow extraction into **standalone, HACS‑installable packages** in the future.

Planned candidates include:
- 📐 Caravan Leveling (travel‑trailer safe)
- 🔔 Notification & alert framework
- 📶 Connectivity & uplink monitoring
- 🌡️ Climate / zone aggregation templates

These packages will be grouped under:

```
packages_hacs/
```
Each package will include:
- Independent README
- Clear prerequisites
- Auto‑discovery notes
- Versioning & changelog
- HACS‑compatible structure and metadata

This approach allows:
- Clean reuse outside this repository
- Easier community adoption
- Optional installation without the full system

