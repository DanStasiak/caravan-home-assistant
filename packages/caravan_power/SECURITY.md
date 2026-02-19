# Security & Secrets (Power Package)

This package is designed to be safe to publish. **No secrets** should be committed.

## Do NOT commit

### ESPHome
- WiFi SSID / password
- Fallback AP password
- OTA password
- API encryption key
- Any MAC addresses
- Any Victron bindkeys
- Any BLE identifiers that map to your devices

### Home Assistant
- Long-lived access tokens
- Webhook URLs
- Credentials inside `rest` / `command_line` / `shell_command`
- Anything in `secrets.yaml`

## Recommended pattern

1) Keep real secrets in `secrets.yaml` (not committed)
2) Keep `secrets.example.yaml` committed with placeholders
3) Add ignores for secrets and keys
