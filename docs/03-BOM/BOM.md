---
title: Bill of Materials
tags:
- tag1
- tag2
---

## Overview

These are the parts for the RadioLink hub. The design uses through-hole components wherever practical. The OLED module and its ZIF connector are the intentional exceptions.

The schematic file in the KiCad zip uses the part numbers in this table. The schematic image and PDF are the 2026-10-30 plot. That plot does not draw J7. Prices are included only where a vendor price was already recorded. No new distributor SKUs were added. J7 has no price and no footprint.

## Hub Bill of Materials

| **Part** | **Ref** | **Qty** | **Package** | **Function** | **Unit cost** |
|:---|:---|:---:|:---|:---|:---|
| PIC18F57Q43 Curiosity Nano | — | 1 | Module | Hub microcontroller | — |
| EastRising ER-OLED0.96-1.3W | U1 | 1 | FPC module, not soldered to the board | 128 x 64 OLED assembly. Controller on the module is SSD1306. Plugs into J7. This is not a UG-2864HSWEG01. | $2.49 |
| EastRising ER-CON30HT-1 | J7 | 1 | SMD, 30-pin, 0.5 mm, top contact. Footprint **not assigned** | ZIF socket for U1. Top contact matches the module. This is not ER-CON30HB-1. | — |
| LM7805 | U4 | 1 | Package **not verified** on the schematic | 9 V to 5 V. Symbol value is LM7805. | — |
| Microchip MCP1700-3302E/TO | U2 | 1 | TO-92 | 5 V to 3.3 V for the OLED. Pin 1 GND, pin 2 VIN, pin 3 VOUT. | — |
| onsemi 2N7000 | Q1, Q2 | 2 | TO-92 | I2C level shift, one device for SDA and one for SCL. Pin 1 source, pin 2 gate, pin 3 drain. Not a BSS138 footprint. | — |
| Red LED | D4 | 1 | Package **not verified** on the schematic export | Debug indicator. Series resistor R7 is 330 Ω. | — |
| 1N4148 | D1, D2, D3 | 3 | Package **not verified** on the schematic export | Small-signal diodes in the I2C level-shift network | — |
| 1 A fuse | F2 | 1 | Package **not verified** on the schematic export | Protects the 9 V input | — |
| Barrel jack | J1 | 1 | Package **not verified** on the schematic export | 9 V input | — |
| 8-pin socket | J4, J5, J6 | 3 | Through-hole connector, as drawn | UART connectors to the other three boards | — |
| Pushbutton | SW1 | 1 | Package **not verified** on the schematic export | Local debug input on the hub. The user buttons are on board 2. | — |
| Jumper | JP1 | 1 | Package **not verified** on the schematic export | Disconnects power from the OLED | — |

C1 and C2 stay 10 µF. That value is above the MCP1700 minimum of 1.0 µF. **Verify** that their ESR is between 0 Ω and 2.0 Ω. C9 is 0.33 µF and C10 is 0.1 µF. No capacitor value was changed.

The microphone, temperature sensor, user buttons, and speaker are not on this board.
