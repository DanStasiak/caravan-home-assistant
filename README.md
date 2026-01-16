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

## 📸 Screenshots

Screenshots will be added once the main dashboards are finalized:
- Caravan Mobile overview
- Leveling calibration
- Power & climate views

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

Issues, discussions, and pull requests are welcome —  
especially improvements that make the system easier to adapt to other travel trailers.
