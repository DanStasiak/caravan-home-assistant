# ⚡ Caravan Power Package (v1.0.0)

Power monitoring and alerting for a travel trailer / caravan Home Assistant deployment.

## What you get

### Canonical battery signals
- `sensor.caravan_battery_voltage` (V)
- `sensor.caravan_battery_current` (A)
- `sensor.caravan_battery_power` (W)
- `sensor.caravan_battery_soc` (%)
- `sensor.caravan_time_to_go` (min + attributes `hours`, `minutes`)
- `sensor.caravan_power_source` (Mains / Alternator / Battery / Unknown)
- `sensor.caravan_battery_ui_status` (OK / CHARGING / ATTENTION)

### Health & freshness
- `sensor.caravan_power_heartbeat` updates every 30s
- `binary_sensor.caravan_power_package_healthy` (Problem=ON when heartbeat stale)
- Freshness signals expected from ESPHome:
  - `binary_sensor.smartshunt_data_fresh`
  - `binary_sensor.victron_ip22_data_fresh`

## Install

Copy into your repo:

```
packages/caravan_power/
```

Enable packages (example):

```yaml
homeassistant:
  packages: !include_dir_named packages
```

Restart Home Assistant.

## Lovelace

- `lovelace/caravan-power-subview.yaml` (Power subview baseline; you can expand it)

## ESPHome (GitHub-safe)

- `esphome/caravan-env-1.github.yaml` (sanitized placeholders, no secrets)

## Changelog

### v1.0.0 (2026-02-19)
- GitHub-ready Power package extraction
- Standardized freshness entities to:
  - `binary_sensor.smartshunt_data_fresh`
  - `binary_sensor.victron_ip22_data_fresh`
