# 🚐 Caravan Home Assistant
### Smart Mobile Trailer platform powered by Home Assistant (Hobby Excellent 540 FU reference)

Turn a **travel trailer (caravan / Wohnwagen)** into a **fully monitored, remotely accessible, and extensible smart system** using **Home Assistant**, **ESPHome**, and open standards.

This repository is a **reference implementation** for a **Hobby Excellent 540 FU (2019)**, designed to be **easy to adapt** to other trailers by swapping hardware mappings and a few entity names.

> ✅ Designed for **travel trailers**
>
> ❌ Not intended for motorhomes  
> ❌ No 4-point leveling logic (front-only leveling for travel trailers)

---

## What you get

- ⚡ **Power & Energy**: battery voltage/current/SOC, charging state, alerts, prepared for AGM → LiFePO₄
- 🌡️ **Climate & Zones**: indoor zones + outside temp, alerting, prepared for Truma Bluetooth path
- 💡 **Lighting**: centralized control (Zigbee-first)
- 🚰 **Water**: tank level monitoring without drilling (ESPHome)
- 📍 **GPS & Location**: auto-detect GPS tracker entity and location display
- 📶 **Connectivity**: WAN monitoring, Starlink + LTE failover awareness, GL.iNet router integration
- 📊 **Mobile-first dashboards**: clean UI with **OK / Attention / Alarm** severity model
- 🔔 **Notification framework**: push + optional TTS, quiet hours, suppression, severity behavior
- 🧩 **ESPHome nodes**: modular ESP32 configs + 3D-printable enclosure STLs

---

## Screenshots
> Add your dashboard screenshots here (recommended for HACS listing quality).

---

## Quick start

### 1) Prerequisites
- Home Assistant (recent version)
- ESPHome (add-on or external)
- Zigbee2MQTT (optional, if using Zigbee devices)
- MQTT broker (required if you use Zigbee2MQTT; recommended anyway)
- HACS (optional but recommended)

---

## Installation

### Option A — Install via HACS (recommended)
This repo is primarily a **YAML “package-style” HA project** (not a traditional custom component).
HACS is used here as an easy distribution/upgrade mechanism.

1. Open **HACS → Integrations → ⋮ → Custom repositories**
2. Add this repository URL and select category **Integration**
3. Install / Download
4. Copy the delivered folders into your HA config (see **File layout** below)
5. Restart Home Assistant

> Tip: If you already keep your HA config in Git, you can skip HACS and just pull the repo content into your config repo.

### Option B — Manual install (Git)
1. Clone or download this repo
2. Copy files into your Home Assistant `/config` directory following the layout below
3. Restart Home Assistant

---

## File layout (where files go)

This repository is structured so it can be copied into your Home Assistant config folder.

Suggested Home Assistant layout:

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

Copy from this repo into the matching locations in `/config`.

---

## Required Home Assistant configuration

### Enable packages (recommended)
In `configuration.yaml`:

```yaml
homeassistant:
  packages: !include_dir_merge_named packages
```

### Include templates / scripts (if you keep them split)
If you use split files:

```yaml
template: !include templates.yaml
script: !include scripts.yaml
automation: !include automations.yaml
```

> If you already have these includes in place, do not duplicate them.

---

## Auto-discovery (how devices “just appear”)

### ESPHome
- ESPHome devices are discovered automatically via **mDNS / API**.
- After flashing a node, you should see it in:
  **Settings → Devices & services → Integrations → ESPHome**
- If you run ESPHome as an add-on, “Adopt” is typically one click.

### Zigbee2MQTT
- Zigbee devices appear via **MQTT discovery** when Zigbee2MQTT is configured.
- Confirm MQTT discovery is enabled in Zigbee2MQTT and your broker is reachable.

### Bluetooth (Truma / sensors)
- Bluetooth integrations depend on your BT adapter / proxy setup.
- If you use ESPHome Bluetooth proxies, they will appear under ESPHome once adopted.

### Dashboards
This repo provides dashboards in `dashboards/`.
You can either:
- Import YAML dashboards in **Settings → Dashboards**, or
- Use YAML mode for dashboards and include them from `dashboards/`.

---

## Key dashboards & UX model

### Severity model
The UI and automation logic follows a simple model:

- ✅ **OK**: everything normal
- 🟧 **Attention**: action needed soon
- 🟥 **Alarm**: urgent / safety / critical

This maps cleanly to:
- badges and chips on the mobile dashboard
- alert notifications
- optional TTS behavior (quiet hours respected)

---

## Notifications & Alerts

Central notification abstraction supports:
- Push notifications
- Optional TTS
- Quiet hours
- Suppression / maintenance mode
- Severity-based behavior

Entry points typically live in:
- `scripts/` (e.g. notify script)
- `packages/alerts/`

---

## Leveling (travel trailers)
Front-only leveling:
- IMU-based ESPHome node
- Calibration UI
- No 4-point leveling automation

Look in:
- `packages/leveling/`
- `esphome/` (IMU node)
- `dashboards/` (level view)

---

## Hardware (reference build)

Reference platform:
- Raspberry Pi 4 running Home Assistant OS
- ESP32 nodes (ESPHome)
- IMU for leveling
- Temperature sensors (zones + outside)
- Zigbee coordinator (optional)
- GL.iNet router (WAN / failover monitoring)
- Optional Starlink

3D prints:
- STL enclosure files in `hardware/stl/`

---

## Adapting to other caravans
Reusable across most trailers:
- dashboards
- alert/notify framework
- connectivity logic
- ESPHome patterns

Trailer-specific adjustments:
- lighting zones and device IDs
- water tank wiring/probes
- physical sensor placement
- entity names (if you don’t keep the same naming conventions)

---

## Troubleshooting
- **Entities missing?** Check that your `packages:` include is enabled and HA was restarted.
- **Zigbee devices not appearing?** Verify MQTT broker + Zigbee2MQTT discovery.
- **ESPHome nodes not found?** Ensure same network, mDNS works, and HA can reach the device.

---

## Project status
- Core systems: **Production**
- Some integrations: **Lab / in progress**
- Actively developed

---

## Disclaimer
This is a DIY project. You are responsible for:
- electrical safety
- regulatory compliance
- any physical modifications

Provided **as-is**, without warranty.

---

## Contributing
Issues and PRs are welcome—especially improvements that make adaptation to non-Hobby trailers easier.
