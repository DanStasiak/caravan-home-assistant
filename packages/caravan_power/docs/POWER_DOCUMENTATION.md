# Mobile Assistant – Power Subsystem Documentation

This document provides a high-level technical description of the Caravan Power subsystem.

## Design Goals

- Deterministic source prioritization
- BLE freshness protection
- Low database churn
- Production-safe automation logic
- Hardware abstraction

## Operational Model

Primary measurement: SmartShunt  
Fallback: BMS  
Conditional fallback: IP22 (fresh only)

## Monitoring Strategy

- Voltage change statistics over 15 minutes
- Charging state inference
- Source classification
- Alert escalation

## Security Model

- No secrets committed
- Placeholder ESPHome config
- Secrets.example.yaml provided
