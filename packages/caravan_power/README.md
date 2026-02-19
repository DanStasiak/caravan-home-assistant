# ⚡ Caravan Power

![Home Assistant](https://img.shields.io/badge/Home%20Assistant-Compatible-blue)
![Package](https://img.shields.io/badge/Type-HA%20Package-green)
![Status](https://img.shields.io/badge/Status-Stable-brightgreen)



> Mobile Assistant – Power Subsystem  
> Structured Victron-based battery monitoring for caravans

---

## 📸 Screenshots

Screenshots are stored in:

```
packages/caravan_power/screenshots/
```

| Overview | Charging | Battery | Mains |
|----------|----------|----------|--------|
| ![](screenshots/power-overview.png) | ![](screenshots/power-charging.png) | ![](screenshots/power-battery.png) | ![](screenshots/power-mains.png) |

---

# 🎯 Overview

The **Caravan Power** package provides a production-ready power intelligence layer for the Mobile Assistant platform.

It unifies battery metrics, charging detection and power source logic into a clean, reusable Home Assistant package.

---

# 🧠 Architecture

## Signal Priority Model

SmartShunt → Primary source  
BMS → Secondary fallback  
IP22 → Used only if data fresh  

Freshness entities required:

- `binary_sensor.smartshunt_data_fresh`
- `binary_sensor.victron_ip22_data_fresh`

---

## Logical Flow

Victron SmartShunt (BLE)  
Victron IP22 Charger (BLE)  
JBD / Humsienk BMS (BLE)  
ESP32 (ESPHome)  
Home Assistant  
Caravan Power Package  
Dashboard + Notifications  

---

# 🔌 Hardware Used

| Component | Purpose |
|------------|----------|
| Victron SmartShunt | Authoritative battery measurement |
| Victron IP22 Charger | Shore charging |
| JBD / Humsienk BMS | Internal LiFePO4 telemetry |
| ESP32 (ESPHome) | BLE bridge + freshness tracking |
| Zigbee Plug | Shore power detection |
| Home Assistant | Automation + UI layer |

Optional:
- Victron Orion DC‑DC (alternator charging)

---

# 🔧 Wiring Concept

Diagrams should be placed in:

```
packages/caravan_power/docs/
```

Conceptual layout:

230V Shore → IP22 → Battery  
Battery → SmartShunt → DC Bus → Loads  

SmartShunt must be installed on the negative battery line.  
ESP32 must be within stable BLE range.

---

# 📁 Folder Structure

```
packages/
  caravan_power/
    caravan_power.yaml
    README.md
    SECURITY.md
    secrets.example.yaml
    lovelace/
    esphome/
    screenshots/
    docs/
```

---

# ⚙ Installation

1. Copy folder into:

```
config/packages/caravan_power/
```

2. Ensure packages are enabled:

```yaml
homeassistant:
  packages: !include_dir_named packages
```

3. Restart Home Assistant.

---

# 📊 Exposed Entities

## Canonical Battery

- `sensor.caravan_battery_voltage`
- `sensor.caravan_battery_current`
- `sensor.caravan_battery_power`
- `sensor.caravan_battery_soc`
- `sensor.caravan_time_to_go`

## Power Intelligence

- `sensor.caravan_power_source`
- `binary_sensor.caravan_mains_present`
- `binary_sensor.caravan_battery_charging_now`
- `binary_sensor.caravan_alternator_charging`
- `binary_sensor.caravan_battery_draining_fast`

## Health

- `sensor.caravan_power_heartbeat`
- `binary_sensor.caravan_power_package_healthy`

---

# 🚨 Alerts

### Critical Battery

Triggered when:

- SoC = Critical  
- Not charging  
- No mains present  

### Draining Fast

Triggered when:

- 15‑minute voltage delta ≤ -0.20V  
- No active charge source  

---

# 📉 Database Optimization

Implements the **Reduce Sensor Logging DB** strategy:

- Trigger-based templates  
- Statistics integration (15m delta)  
- ESPHome delta filtering  
- Single BLE heartbeat per device  

Result: minimal database churn with high UI responsiveness.

---

# 🔐 Security

This package contains **no secrets**.

See:

- `SECURITY.md`
- `secrets.example.yaml`

Never commit:

- WiFi credentials  
- MAC addresses  
- Bindkeys  
- API encryption keys  
- OTA passwords  

---

# 📦 Version

**v1.0.0**  
Released: 2026-02-19

Initial standalone Power package extraction from the Mobile Assistant project.
