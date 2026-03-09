# 5.8 GHz Add-on Module

Optional module that adds analog and digital 5.8 GHz detection and video viewing.

## Key Components

| Part | Function | Interface |
|------|----------|-----------|
| RTL8812AU | 5 GHz 802.11ac monitor mode | USB 3.0 |
| RX5808 | Analog 5.8 GHz RX + RSSI | SPI |
| ADV7280A-M | Analog composite video decoder | I2C |
| 2x IPEX U.FL | Antenna connectors (RTL8812AU) | — |
| 1x IPEX U.FL | Antenna connector (RX5808) | — |
| 10-pin FPC | Connection to base module | — |

## What It Detects

| Signal | Method | Video? |
|--------|--------|--------|
| Analog FPV video | RX5808 RSSI sweep | Yes — streams to web UI |
| WFB-ng / OpenHD / OpenIPC | RTL8812AU monitor mode | Yes — wfb_rx decode |
| DJI OcuSync 5.8 / O3 | RTL8812AU monitor mode | No — detection only |
| 5 GHz WiFi drones | RTL8812AU monitor mode | No — detection only |

## Connector (FPC 10-pin 2mm pitch)

| Pin | Signal |
|-----|--------|
| 1–2 | GND |
| 3–4 | 5V power from base |
| 5–6 | USB 3.0 D+/D- (RTL8812AU) |
| 7 | SPI CLK (RX5808) |
| 8 | SPI MOSI (RX5808) |
| 9 | SPI CS (RX5808) |
| 10 | I2C SDA (ADV7280A-M) |

## Antennas

- RTL8812AU: 2x 5.8 GHz SMA via IPEX pigtail
- RX5808: 1x 5.8 GHz SMA via IPEX pigtail

## Size

Target PCB: 40x35mm
