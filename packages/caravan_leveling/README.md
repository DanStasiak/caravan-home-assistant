# 📐 Travel Trailer Leveling (Front Axle) – Home Assistant Package

**Repository:** `caravan-home-assistant`  
**Package:** `caravan_leveling`  
**Version:** `v1.1.0`  
**Scope:** **Travel trailers / caravans with a single axle (two wheels)**

🔗 **Project root:**  
https://github.com/DanStasiak/caravan-home-assistant

This package provides a calibrated **front‑axle leveling assistant** using **two IMU sensors**:
- **Front Left (FL)** – mounted just in front of the left tire  
- **Front Right (FR)** – mounted just in front of the right tire  

It produces a single combined front‑axle leveling status (**LEVEL / ATTENTION / ALARM**), plus actionable guidance and a calibration wizard.

> ⚠️ This is a **manual guidance system**  
> ❌ No actuator control  
> ❌ No automatic leveling  
> ❌ No motorhomes / no 4‑point systems

---

## 📸 Screenshots

### Level (main)
![Level view](./screenshots/level.png)

### Calibration Wizard
![Calibration view](./screenshots/level-calibration.png)

---

## 🧭 Architecture (Leveling Package)

```
        ┌───────────────┐
        │   ESP32 /     │
        │   ESP8266     │
        │   (ESPHome)   │
        └───────┬───────┘
                │ I²C
        ┌───────▼───────┐
        │     IMU       │
        │  MPU6050 etc  │
        └───────┬───────┘
                │ WiFi
        ┌───────▼─────────────┐
        │   Home Assistant    │
        │  - Template sensors │
        │  - Helpers          │
        │  - Calibration      │
        │  - Lovelace UI      │
        └─────────────────────┘
```

**Data flow**
1. IMUs measure pitch/roll
2. ESPHome exposes sensors
3. Home Assistant stores a *level reference*
4. UI shows deviation + status

---

## 🧾 Wiring Diagram (SVG)

![Wiring diagram](./docs/wiring.svg)

---

## 🧰 Hardware Used

### Front Right (FR)
- **MCU:** ESP8266 NodeMCU v2  
- **IMU:** GY‑521 / **MPU6050** (I²C)  
- **Optional ambient sensor:** **SHT3x** (I²C, shared bus)  
- **Enclosure:** Custom 3D‑printed case + top (STL)

### Front Left (FL)
- **MCU:** **ESP32 Dev Module**  
- **IMU:** GY‑521 / **MPU6050** (I²C)  
- **Optional ambient sensor:** **SHT3x** (I²C, shared bus)  
- **Enclosure:** Custom 3D‑printed case + top (STL)

---

## ✅ Home Assistant Prerequisites

- Home Assistant **2024.10+**
- ESPHome **2024.12+**
- YAML configuration enabled

---

## 📦 Frontend Plugins (UI only)

Install via **HACS → Frontend**:

- **Mushroom Cards**  
  https://github.com/piitaya/lovelace-mushroom
- **bar-card**  
  https://github.com/custom-cards/bar-card
- **card-mod**  
  https://github.com/thomasloven/lovelace-card-mod

Restart Home Assistant after installation.

---

## 🧩 Installation (Home Assistant YAML Package)

This package is **not installed via HACS**.  
It is a **YAML package** placed inside your HA config.

### Steps

1. Copy this folder:
   ```
   packages/caravan_leveling/
   ```
2. Ensure packages are enabled:
   ```yaml
   homeassistant:
     packages: !include_dir_named packages
   ```
3. Restart Home Assistant

---

## 🧩 ESPHome Auto‑Discovery & Stable Entity IDs

### Recommended (best)
Use the provided ESPHome files:
- `esphome/caravan_level_front_right_fr.yaml`
- `esphome/caravan_level_front_left_fl.yaml`

This guarantees stable entities such as:
- `sensor.caravan_level_front_right_fr_pitch_level_ref`
- `sensor.caravan_level_front_left_fl_pitch_level_ref`

### Existing devices
Rename ESPHome device names to:
- `caravan_level_front_right_fr`
- `caravan_level_front_left_fl`
Then restart Home Assistant.

---

## 🖥 Lovelace UI

Import:
- `lovelace/caravan-level.yaml`
- `lovelace/caravan-level-calibration.yaml`

Mobile‑first, outdoor‑readable, large touch targets.

---

## 🔔 Notifications (Blueprint)

Blueprint:
- `blueprints/automation/caravan_leveling_notify.yaml`

Features:
- Alerts on **ATTENTION / ALARM**
- Optional recovery notification
- Suppression while moving
- Cooldown logic
- Deep link to leveling dashboard

---

## 🧱 3D‑Printed Enclosure (STL)

```
stl/
├─ caravan_level_sensor_case.stl
└─ caravan_level_sensor_top.stl
```

Printing notes:
- PETG or ABS recommended
- 0.2 mm layer height
- ≥3 perimeters
- Rigid mounting (no foam)

---

## ⚠️ Common Mistakes & Troubleshooting

### ❌ IMU mounted loosely
➡️ Causes drifting and inconsistent readings  
✔️ Mount rigidly to the caravan structure

### ❌ Wrong IMU orientation
➡️ Front/back axis inverted  
✔️ Adjust axis mapping in ESPHome YAML

### ❌ Calibrating on uneven ground
➡️ “Level” reference becomes wrong  
✔️ Always calibrate on a known level surface

### ❌ Re‑using old reference after hardware change
➡️ Offsets no longer valid  
✔️ Reset and recalibrate after any sensor move

### ❌ Expecting automatic leveling
➡️ This is manual guidance only  
✔️ Adjust jockey wheel / ramps yourself

---

## 🚫 Scope (By Design)

- Single‑axle travel trailers only
- No motorhomes
- No motorized actuators
- No 4‑point leveling

This keeps the system **safe, predictable, and portable**.

---

## 🏷 Versioning

- **v1.1.0**
  - Documentation polish
  - Architecture diagram
  - Troubleshooting section
  - Root README cross‑link
- **v1.0.0**
  - Front axle leveling (FL + FR)
  - Calibration wizard
  - Lovelace UI
