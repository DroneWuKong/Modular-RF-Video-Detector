# Modular RF Video Detector

**Compact, modular RF detector and FPV video monitor built around the Radxa Zero 3W**

![License](https://img.shields.io/badge/license-GPLv3-blue.svg)
![Status](https://img.shields.io/badge/status-design--phase-yellow.svg)

> **Status: Design-phase scaffold.** This repo currently contains documentation and project structure only — hardware files (BOMs, KiCAD, 3D models) and software (scanner code, `setup.sh`) are not yet implemented.

## Overview

A modular RF detection and FPV video monitoring platform covering 150 MHz to 5.8 GHz. Designed around the Radxa Zero 3W running Linux, with a hot-swappable 5.8 GHz add-on module for analog and digital video reception.

**Base Unit covers:**
- 150–960 MHz sub-GHz (CC1101 or SX1262)
- 2.4 GHz WiFi monitor mode (built-in Radxa radio)
- BLE 5.0
- GPS logging
- Web UI, TAK integration, ESP-NOW mesh

**5.8 GHz Add-on Module adds:**
- 5 GHz digital monitor mode (RTL8812AU)
- Analog 5.8 GHz detection + video (RX5808)
- WFB-ng / OpenHD / OpenIPC video viewing
- Streams video to phone/tablet via web UI

## Architecture

```
┌─────────────────────────────────────┐
│           BASE MODULE               │
│  Radxa Zero 3W                      │
│  CC1101 / SX1262 (sub-GHz SPI)     │
│  GPS (UART)                         │
│  OLED display (I2C)                 │
│  LiPo + USB-C charging             │
│  2.4 GHz monitor mode (built-in)   │
│  BLE + Web UI + TAK                │
│  [Module Port — FPC connector] ───►│
└─────────────────────────────────────┘
                │
                ▼ (optional)
┌─────────────────────────────────────┐
│        5.8 GHz ADD-ON MODULE        │
│  RTL8812AU — 5 GHz monitor mode    │
│  RX5808 — analog RX + video        │
│  ADV7280A-M — video decoder        │
│  2x IPEX antenna connectors        │
└─────────────────────────────────────┘
```

## Key Hardware

**Base Module:**
- Radxa Zero 3W (RK3566, 2GB RAM, eMMC, dual-band WiFi, BLE 5.0)
- CC1101 or SX1262 sub-GHz module
- NEO-6M GPS
- SSD1306 OLED 128x64
- Single cell LiPo + USB-C PD charging

**5.8 GHz Add-on:**
- RTL8812AU (USB 3.0 to Radxa)
- RX5808 analog 5.8 GHz receiver
- ADV7280A-M analog video decoder
- 2x IPEX U.FL connectors

## Video Support

| Source | Detection | Video |
|--------|-----------|-------|
| Analog FPV (5.8 GHz) | RX5808 | Stream via web UI |
| WFB-ng / OpenHD / OpenIPC | RTL8812AU monitor | Stream via web UI |
| DJI OcuSync / O3 | RTL8812AU monitor | Detection only |
| 2.4 GHz WiFi drones | Built-in radio | Detection only |

Video streams to browser on phone/tablet — no physical screen required.

## Repository Structure

See `FOLDER_STRUCTURE.md` for full layout.

## Build Options

- **Base only** — sub-GHz + 2.4 GHz detection, BLE, TAK, web UI
- **Base + 5.8 add-on** — full spectrum coverage + analog/digital video

## Power

- Single cell LiPo (3.7V) with 5V boost
- USB-C PD input — charge from any USB-C power bank
- No 12V required
- Estimated runtime: 3–4 hours (base only), 2–3 hours (with add-on)

## Status

Design-phase scaffold. Documentation and project structure are in place; hardware design files and software are not yet implemented.

## License

GNU General Public License v3.0 (GPLv3) — see the [LICENSE](LICENSE) file.
