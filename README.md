# zigbee2mqtt-doctor

**Live diagnostic dashboard for Zigbee2MQTT — device health, LQI monitoring, offline detection, and troubleshooting guidance.**

[![License: MIT](https://img.shields.io/badge/License-MIT-7c3aed.svg)](LICENSE)

![Demo](demo.gif)

---

## Usage

**Option A — Open locally:**

1. Clone or download this repo.
2. Open `index.html` in Chrome or Edge (Firefox works too).
3. Enter your Zigbee2MQTT host and port (e.g. `192.168.1.10:8080`).
4. Click **Connect**.

**Option B — GitHub Pages live demo:**

Visit: **https://MJFlanigan5.github.io/zigbee2mqtt-doctor/**

> **Note:** If your Z2M instance uses `http://`, open the GitHub Pages URL over `http://` or serve `index.html` locally. Browsers block mixed-content WebSocket connections (`ws://` from an `https://` page).

---

## Features

- **Zero dependencies** — pure vanilla HTML/CSS/JS, no build step, no Node.js required
- **Live WebSocket connection** to Zigbee2MQTT with auto-reconnect
- **Bridge panel** — coordinator type, firmware version, Zigbee channel, PAN ID, permit-join status
- **Devices table** — sortable by name, type, LQI, or last-seen; filterable by All / Offline / Low LQI; search by name
- **LQI signal bars** — color-coded (green ≥ 100, yellow 50-99, red < 50) with numeric value
- **Last-seen relative timestamps** — "2m ago", "3h ago", "2d ago", refreshed every 30 s
- **Diagnostics panel** — auto-checks with fix hints:
  - Coordinator online/offline
  - Permit join enabled warning
  - Devices offline > 24 h
  - Devices with critically weak signal (LQI < 30)
  - Devices never fully interviewed
  - End devices with no router in the network
- **Per-device Interview button** — re-trigger Z2M interview via WebSocket command
- **Permit Join toggle** — enable for 60 s or disable from the toolbar
- **Live log stream** — color-coded by level (info / warning / error / debug), auto-scroll, clearable
- **CSV export** — download all device data as a spreadsheet
- **Dark theme** — comfortable for long sessions
- Remembers your last host:port in `localStorage`

---

## Setup — Zigbee2MQTT requirements

The Z2M frontend WebSocket must be enabled. Add this to your `configuration.yaml`:

```yaml
frontend:
  port: 8080          # default; change if needed
  # host: 0.0.0.0    # uncomment to expose on all interfaces
```

Restart Zigbee2MQTT after editing. Verify by opening `http://<your-host>:8080` in a browser — you should see the Z2M web UI.

The doctor app connects to `ws://<host>:<port>/api`, the same endpoint the official frontend uses.

---

## File structure

```
zigbee2mqtt-doctor/
├── index.html    — Complete single-file app (HTML + CSS + JS)
├── README.md
├── LICENSE       — MIT
└── .gitignore
```

---

## MIT License

Copyright (c) 2026 Michael Flanigan. See [LICENSE](LICENSE) for details.
