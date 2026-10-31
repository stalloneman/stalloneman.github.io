---
title: Bill of Materials
tags:
- tag1
- tag2
---

## Overview

These are the parts for the RadioLink hub. The design uses through-hole components wherever practical. The OLED module is an intentional exception.

The current KiCad export has not been updated yet. It still shows a UG-2864HSWEG01 symbol, BSS138 MOSFETs, and a 5-pin U2. This table is the intended orderable list. Prices are included only where a vendor price was already recorded. No new distributor SKUs were added.

## Hub Bill of Materials

| **Part** | **Ref** | **Qty** | **Package** | **Function** | **Unit cost** |
|:---|:---|:---:|:---|:---|:---|
| PIC18F57Q43 Curiosity Nano | — | 1 | Module | Hub microcontroller | — |
| EastRising ER-OLED0.96-1.3W | U1 | 1 | FPC module, not through-hole | 128 x 64 OLED assembly. Controller on the module is SSD1306. This is not a UG-2864HSWEG01. | $2.49 |
| STMicroelectronics L7805CV | U4 | 1 | TO-220 | 9 V to 5 V | ~$1.08 |
| Microchip MCP1700-3302E/TO | U2 | 1 | TO-92 | 5 V to 3.3 V for the OLED. Pin 1 GND, pin 2 VIN, pin 3 VOUT. | — |
| onsemi 2N7000G | Q1, Q2 | 2 | TO-92 | I2C level shift, one device for SDA and one for SCL. Pin 1 source, pin 2 gate, pin 3 drain. Not a BSS138 footprint. | — |
| Red LED | D4 | 1 | Package **not verified** on the schematic export | Debug indicator. Series resistor R7 is 330 Ω. | — |
| 1N4148 | D1, D2, D3 | 3 | Package **not verified** on the schematic export | Small-signal diodes in the I2C level-shift network | — |
| 1 A fuse | F2 | 1 | Package **not verified** on the schematic export | Protects the 9 V input | — |
| Barrel jack | J1 | 1 | Package **not verified** on the schematic export | 9 V input | — |
| 8-pin socket | J4, J5, J6 | 3 | Through-hole connector, as drawn | UART connectors to the other three boards | — |
| Pushbutton | SW1 | 1 | Package **not verified** on the schematic export | Local debug input on the hub. The user buttons are on board 2. | — |
| Jumper | JP1 | 1 | Package **not verified** on the schematic export | Disconnects power from the OLED | — |

C1 and C2 stay 10 µF. That value is above the MCP1700 minimum of 1.0 µF. **Verify** that their ESR is between 0 Ω and 2.0 Ω. C9 is 0.33 µF and C10 is 0.1 µF, which matches the L7805C datasheet test circuit. No capacitor value was changed.

The microphone, temperature sensor, user buttons, and speaker are not on this board.
