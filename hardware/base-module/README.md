# Base Module

Radxa Zero 3W based RF detection platform.

## Key Components

| Part | Function | Interface |
|------|----------|-----------|
| Radxa Zero 3W | Main SoC, 2.4/5 GHz WiFi, BLE | — |
| CC1101 or SX1262 | Sub-GHz 150–960 MHz | SPI |
| NEO-6M GPS | Location logging | UART |
| SSD1306 OLED 128x64 | Status display | I2C |
| LiPo cell (3.7V) | Battery | — |
| USB-C PD IC | Charging + power input | — |
| 5V boost converter | LiPo → 5V system rail | — |
| 10-pin FPC connector | Add-on module port | USB+SPI+I2C |

## Pinout (Radxa Zero 3W GPIO)

| GPIO | Function |
|------|----------|
| SPI0 CLK | CC1101/SX1262 SCK |
| SPI0 MOSI | CC1101/SX1262 MOSI |
| SPI0 MISO | CC1101/SX1262 MISO |
| GPIO X | CC1101/SX1262 CS |
| GPIO X | CC1101 GDO0 / SX1262 DIO1 |
| I2C SDA | OLED SDA |
| I2C SCL | OLED SCL |
| UART TX | GPS RX |
| UART RX | GPS TX |
| USB 3.0 | FPC add-on (RTL8812AU) |

Full pin assignments TBD during PCB layout.

## Power

- Input: USB-C PD (5V)
- Battery: Single cell LiPo 3.7V
- System rail: 5V (boost converter)
- 3.3V: Radxa onboard LDO for peripherals

## Size

Target PCB: 70x35mm (accommodates Radxa Zero 3W + connectors)
