# 🚐 Travel Trailer Leveling (Front Axle) – Home Assistant Package

**Repository:** `caravan-home-assistant`  
**Package:** `caravan_leveling`  
**Version:** `v1.0.0`  
**Scope:** **Travel trailers / caravans with a single axle (two wheels)**

This package provides a calibrated leveling system using **two IMU sensors**:
- **Front Left (FL)** – mounted just in front of the left tire
- **Front Right (FR)** – mounted just in front of the right tire

It produces a single combined front-axle leveling status (**LEVEL / ATTENTION / ALARM**), plus actionable guidance and a calibration wizard.

---

## 📸 Screenshots

### Level (main)
![Level view](./screenshots/level.png)

### Calibration Wizard
![Calibration view](./screenshots/level-calibration.png)

---

## 🧭 System Overview

**Front axle layout (single axle / two wheels):**

```
FRONT OF TRAILER
┌───────────────────────────────┐
│                               │
│   [ FL SENSOR ]   [ FR SENSOR ]│
│     (left)          (right)   │
│                               │
└───────── O ───────── O ────────┘
          Left        Right
          Wheel       Wheel
```

The sensors measure pitch/roll relative to a calibrated reference. Home Assistant combines both into a reliable front leveling result.

---

## 🧰 Hardware Used

### Front Right (FR)
- **MCU:** ESP8266 NodeMCU v2  
- **IMU:** GY-521 / **MPU6050** (I²C)  
- **Optional ambient sensor:** **SHT3x** (I²C, shared bus)  
- **Enclosure:** Custom 3D‑printed case + top (STL)

### Front Left (FL)
- **MCU:** **ESP32 Dev Module**  
- **IMU:** GY-521 / **MPU6050** (I²C)  
- **Optional ambient sensor:** **SHT3x** (I²C, shared bus)  
- **Enclosure:** Custom 3D‑printed case + top (STL)

---

## 🧱 3D‑Printed Enclosure (STL)

```
stl/
├─ caravan_level_sensor_case.stl
└─ caravan_level_sensor_top.stl
```

**Printing recommendations**
- PETG or ABS (PLA not recommended for caravans)
- 0.2 mm layer height
- ≥3 perimeters
- Rigid mounting (no foam between IMU and case)

> ⚠️ Sensor orientation must not change after calibration.

---

## 🔌 Wiring Diagrams

### ESP8266 (NodeMCU v2) ↔ MPU6050

```
NodeMCU (ESP8266)     MPU6050
-----------------------------
3V3  ---------------> VCC
GND  ---------------> GND
D2 (GPIO4) ---------> SDA
D1 (GPIO5) ---------> SCL
```

### ESP32 ↔ MPU6050

```
ESP32                 MPU6050
-----------------------------
3V3  ---------------> VCC
GND  ---------------> GND
GPIO21 -------------> SDA
GPIO22 -------------> SCL
```

SHT3x (optional) shares the same I²C bus.

---

## ✅ Home Assistant Prerequisites

- Home Assistant **2024.10+**
- ESPHome **2024.12+**
- YAML configuration enabled

---

## 📦 HACS Frontend Plugins (Required)

Install via **HACS → Frontend**:

- Mushroom Cards  
  https://github.com/piitaya/lovelace-mushroom

- bar-card  
  https://github.com/custom-cards/bar-card

- card-mod  
  https://github.com/thomasloven/lovelace-card-mod

Restart Home Assistant after installation.

---

## 🧠 What This Package Provides

### Sensors
- `sensor.caravan_front_level_state`
- `sensor.caravan_front_tilt_max`
- `sensor.caravan_front_pitch_avg`
- `sensor.caravan_front_roll_avg`

### Scripts
- `script.caravan_front_level_set_reference`
- `script.caravan_front_level_reset_reference`
- `script.caravan_front_level_calibration_wizard`

### UI
- Level view
- Calibration wizard view

### ESPHome
- Full YAML configs for FR (ESP8266) and FL (ESP32) nodes

---

## 🧪 Calibration Flow

1. Park trailer on visually level ground  
2. Ensure trailer is not moving  
3. Open **Level Calibration**  
4. Press **One‑tap wizard** (Reset → wait → Set)

Calibration timestamp is stored in:
- `input_datetime.caravan_front_level_last_calibration`

---

## 🧩 Installation

1. Copy package:
   ```
   packages/caravan_leveling/
   ```

2. Enable packages in `configuration.yaml`:
   ```yaml
   homeassistant:
     packages: !include_dir_named packages
   ```

3. Restart Home Assistant

4. Import Lovelace views from:
   ```
   packages/caravan_leveling/lovelace/
   ```

5. Flash ESPHome nodes using configs in:
   ```
   packages/caravan_leveling/esphome/
   ```

---

## 🚫 Scope (By Design)

This project is intentionally limited to **travel trailers / caravans with a single axle**.  
No 4‑point or motorized leveling systems are supported or planned.

---

## Versioning

- **v1.0.0** – Front axle leveling (FL + FR), calibration wizard, Lovelace UI
