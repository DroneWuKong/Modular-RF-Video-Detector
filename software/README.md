# Software

All software runs on the Radxa Zero 3W under Debian/Ubuntu.

> **Planned — not yet implemented.** This document describes the intended
> software layout. No scanner code, web UI, or `setup.sh` exists in the repo
> yet; the components and quick-start below are design targets.

## Components

| Component | Language | Purpose |
|-----------|----------|---------|
| rf-scanner | Python/C | CC1101/SX1262 sub-GHz scanning daemon |
| wifi-scanner | Python | 2.4/5 GHz monitor mode scanning |
| rx5808-scanner | Python | Analog 5.8 GHz RSSI sweep (add-on) |
| wfb_rx | C (upstream) | WFB-ng video receive (add-on) |
| web | Python/JS | Unified web UI + WebRTC video streaming |
| tak-sender | Python | CoT UDP output to TAK server |

## Quick Start (planned)

Once `setup.sh` is implemented, setup is intended to be:

```bash
git clone https://github.com/DroneWuKong/Modular-RF-Video-Detector
cd Modular-RF-Video-Detector/software/base
sudo bash setup.sh   # planned — not yet added
```

## Web UI

Connect to device WiFi AP or local network, open browser:
```
http://[device-ip]:8080
```

Features:
- Live detection dashboard
- Spectrum waterfall
- Video stream viewer (add-on required for 5.8 GHz)
- TAK server configuration
- BLE status
