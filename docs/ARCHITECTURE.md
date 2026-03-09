# System Architecture

## Design Philosophy

- **Modular** — base unit is fully functional standalone; 5.8 GHz add-on snaps on when needed
- **Small** — Radxa Zero 3W (65x30mm) as single brain, no stacked MCU + Linux companion
- **Battery first** — single LiPo cell, USB-C PD, runs off any power bank
- **No screen required** — all video and detection data streams to phone/tablet via web UI

## Block Diagram

```
                    ┌──────────────────────────────────────────┐
                    │              BASE MODULE                  │
                    │                                          │
  Sub-GHz RF ──────►│ CC1101 / SX1262 (SPI)                   │
  GPS ─────────────►│ NEO-6M (UART)                           │
  OLED ────────────►│ SSD1306 (I2C)                           │
  LiPo ────────────►│ 5V boost → USB-C PD                     │
                    │                                          │
                    │      ┌──────────────────────┐           │
                    │      │   Radxa Zero 3W       │           │
                    │      │   RK3566 quad-core    │           │
                    │      │   2GB LPDDR4          │           │
                    │      │   eMMC storage        │           │
                    │      │   2.4+5 GHz WiFi      │◄── 2.4GHz │
                    │      │   BLE 5.0             │           │
                    │      │   USB 3.0 host        │           │
                    │      └──────────────────────┘           │
                    │              │                           │
                    │         [FPC connector]                  │
                    └──────────────┼───────────────────────────┘
                                   │
                    ┌──────────────▼───────────────────────────┐
                    │         5.8 GHz ADD-ON MODULE            │
                    │                                          │
                    │  RTL8812AU ──► USB 3.0 ──► Radxa        │
                    │  RX5808 ────► SPI ──────► Radxa         │
                    │  ADV7280A-M ► I2C ──────► Radxa         │
                    │  2x IPEX antenna connectors              │
                    └──────────────────────────────────────────┘
```

## Radio Coverage

| Band | Hardware | Method | Detects |
|------|----------|--------|---------|
| 150–960 MHz | CC1101 / SX1262 | RSSI scan | ELRS, Crossfire, SiK, LoRa, RFD900 |
| 2.4 GHz | Radxa built-in | Monitor mode | WiFi drones, ELRS 2.4, Ghost, OcuSync |
| 2.4 GHz | Radxa built-in | Promiscuous | WFB-ng, OpenHD, silent drones (OUI) |
| 5 GHz | RTL8812AU (add-on) | Monitor mode | OcuSync 5.8, WFB-ng 5.8, DJI O3 |
| 5.8 GHz analog | RX5808 (add-on) | RSSI sweep | Analog FPV video transmitters |

## Video Pipeline

### Analog (RX5808)
```
RX5808 → composite video out
    → ADV7280A-M (analog-to-digital decoder, I2C)
    → Radxa video capture
    → ffmpeg H.264 encode
    → WebRTC → browser on phone (~100-200ms latency)
```

### Digital WFB-ng / OpenHD / OpenIPC
```
RTL8812AU in monitor mode
    → wfb_rx daemon on Radxa
    → decoded H.264/H.265
    → WebRTC → browser on phone
```

### DJI / Proprietary
```
RTL8812AU in monitor mode
    → frame detection only (encrypted, no video decode)
```

## Software Stack

```
Radxa Zero 3W (Debian/Ubuntu)
├── rf-scanner daemon        # CC1101/SX1262 sub-GHz scanning
├── wifi-scanner daemon      # 2.4/5 GHz monitor mode
├── rx5808-scanner daemon    # Analog 5.8 GHz RSSI sweep (add-on)
├── wfb_rx                   # WFB-ng video receive (add-on)
├── ffmpeg                   # Video encode/stream
├── web server               # Unified web UI
│   ├── detection dashboard
│   ├── spectrum display
│   ├── video stream viewer
│   └── TAK/BLE/config
└── tak-sender               # CoT UDP output
```

## Module Connector (FPC)

10-pin 2mm pitch FPC/FFC connector carries:

| Pin | Signal | Description |
|-----|--------|-------------|
| 1 | GND | Ground |
| 2 | GND | Ground |
| 3 | 5V | Power to add-on |
| 4 | 5V | Power to add-on |
| 5 | USB_DP | RTL8812AU USB 3.0 D+ |
| 6 | USB_DM | RTL8812AU USB 3.0 D- |
| 7 | SPI_CLK | RX5808 SPI clock |
| 8 | SPI_MOSI | RX5808 SPI data |
| 9 | SPI_CS | RX5808 chip select |
| 10 | I2C_SDA | ADV7280A-M video decoder |

Note: I2C_SCL shared with SPI_CLK on pin 7 (time-multiplexed, handled in driver)

## Power Architecture

```
USB-C PD input (5V)
    │
    ├──► Radxa Zero 3W VIN (5V)
    ├──► FPC pin 3/4 → Add-on module (5V)
    └──► LiPo charger IC
              │
              └──► Single cell LiPo (3.7V)
                        │
                        └──► 5V boost converter → system 5V rail
```

No 12V required. No LM2596 buck converter. Runs directly from USB-C power bank.

## Power Budget

| Component | Current @ 5V |
|-----------|-------------|
| Radxa Zero 3W (active) | ~700mA |
| CC1101 / SX1262 | ~100mA |
| OLED + GPS | ~150mA |
| **Base total** | **~950mA** |
| RTL8812AU (add-on) | ~600mA |
| RX5808 (add-on) | ~200mA |
| **With add-on total** | **~1750mA** |

Battery runtime (3000mAh LiPo):
- Base only: ~3–4 hours
- With add-on: ~2–2.5 hours
