# Entity Mapping Guide – Caravan Mobile Start Page

This view is published with **example entities**. Map them to your own installation.

## Sanitisation changes applied

| Original (private) | Published (sanitised) | Why |
|---|---|---|
| `sensor.gps_127_0_0_1_mode` | `sensor.caravan_gps_mode` | Remove internal/host-specific identifier |

## Entities referenced by the start page (examples)

| Entity | Purpose |
|---|---|
| `binary_sensor.caravan_alarm` | Alarm state (true/false) |
| `binary_sensor.caravan_attention` | Attention/warning state (true/false) |
| `binary_sensor.caravan_gps_fix_ok` | GPS fix available/healthy |
| `binary_sensor.caravan_gps_stale` | GPS data stale |
| `binary_sensor.caravan_heater_stale` | Heater telemetry stale/unavailable |
| `binary_sensor.caravan_moving` | Movement/travel state |
| `binary_sensor.failover_active` | WAN failover active (LTE) indicator |
| `binary_sensor.internet_ok` | Internet connectivity health |
| `input_boolean.caravan_heater_connected` | Heater integration connected |
| `input_boolean.caravan_heater_installed` | Heater integration installed/enabled |
| `input_number.caravan_battery_soc` | Battery SoC (%) input/helper |
| `input_number.water_tank_level` | Water tank level (%) input/helper |
| `sensor.caravan_front_level_state` | Level state (LEVEL/ATTENTION/ALARM) |
| `sensor.caravan_front_tilt_max` | Max tilt metric (deg) |
| `sensor.caravan_gps_mode` | GPS mode/status (example) |
| `sensor.caravan_heater_summary` | Heater summary text/status |
| `sensor.caravan_level_pitch` | Pitch (deg) |
| `sensor.caravan_level_roll` | Roll (deg) |
| `sensor.caravan_power_summary` | Power summary text/status |
| `sensor.caravan_temperature_average` | Average interior temperature |
| `sensor.caravan_uplink_router` | Router uplink type/status |
| `sensor.connectivity_quality` | Connectivity quality score/state |
