# Security (Caravan Power Package)

This repository is designed to be safe for public GitHub publishing.

## ✅ Rules
- **Never commit secrets** (WiFi passwords, MAC addresses, bindkeys, API keys, tokens).
- Use `secrets.yaml` for ESPHome credentials and device identifiers.
- Keep Home Assistant packages free of personal identifiers (IPs, usernames, hostnames).

## ESPHome
Use `esphome/caravan-env-1.github.yaml` and populate values via `secrets.yaml`.

## Git Hygiene
Add these to your repo `.gitignore`:
- `secrets.yaml`
- `secrets*.yaml`
- `*.log`
- `*.db`
- `*.sqlite*`
- `.storage/`

## Reporting
If you find a secret in the repo history, rotate it immediately and rewrite history if needed.
