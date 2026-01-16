# 🚐 Travel Trailer Leveling (Front Axle) – Home Assistant Package

**Repository:** `caravan-home-assistant`  
**Package:** `caravan_leveling`  
**Version:** `v1.0.0`  
**Scope:** **Travel trailers / caravans with a single axle (two wheels)**

This package provides a calibrated **front‑axle leveling assistant** using **two IMU sensors**:
- **Front Left (FL)** – mounted just in front of the left tire  
- **Front Right (FR)** – mounted just in front of the right tire  

It produces a single combined front‑axle leveling status (**LEVEL / ATTENTION / ALARM**), plus actionable guidance and a calibration wizard.

> ⚠️ This is a **manual guidance system**.  
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

## 📦 Frontend Plugins (Required)

Install via **HACS → Frontend** (these are UI cards only):

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
It is a **YAML package** meant to live inside your Home Assistant configuration.

### Steps

1. Copy this folder into your HA config:
   ```
   packages/caravan_leveling/
   ```

2. Enable packages in `configuration.yaml` (once):
   ```yaml
   homeassistant:
     packages: !include_dir_named packages
   ```

3. Restart Home Assistant

---

## 🧩 ESPHome Auto‑Discovery & Stable Entity IDs

To work out‑of‑the‑box, the ESPHome nodes must expose **expected entity IDs**.

### Recommended (best)
Use the ESPHome YAML files provided in this repository:
- `esphome/caravan_level_front_right_fr.yaml`
- `esphome/caravan_level_front_left_fl.yaml`

These produce entities such as:
- `sensor.caravan_level_front_right_fr_pitch_level_ref`
- `sensor.caravan_level_front_left_fl_pitch_level_ref`
- calibration buttons and roll/tilt sensors

### Existing devices
If you already have nodes:
- Rename ESPHome devices to:
  - `caravan_level_front_right_fr`
  - `caravan_level_front_left_fl`
- Restart Home Assistant (or re‑add the ESPHome device)

---

## 🖥 Lovelace UI

Import the provided views:
- `lovelace/caravan-level.yaml`
- `lovelace/caravan-level-calibration.yaml`

These views are mobile‑first and optimized for outdoor use.

---

## 🔔 Notifications (Blueprint)

Included blueprint:
- `blueprints/automation/caravan_leveling_notify.yaml`

Features:
- Alerts on **ATTENTION / ALARM**
- Optional recovery notification
- Suppression while moving
- Simple cooldown
- Deep link to the leveling dashboard

---

## 🧱 3D‑Printed Enclosure (STL)

Place STL files here:
```
stl/
├─ caravan_level_sensor_case.stl
└─ caravan_level_sensor_top.stl
```

Printing notes:
- PETG or ABS recommended (PLA not ideal for caravans)
- 0.2 mm layer height, ≥3 perimeters
- Rigid mounting (no foam between IMU and case)

---

## 🚫 Scope (By Design)

This package is intentionally limited to **single‑axle travel trailers**.

- No 4‑point leveling
- No motorized actuators
- No motorhomes

This keeps the system **safe, predictable, and portable**.

---

## 🏷 Versioning

- **v1.0.0** – Front axle leveling (FL + FR), calibration wizard, Lovelace UI
