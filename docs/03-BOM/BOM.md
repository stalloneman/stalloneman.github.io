---
title: Bill of Materials
tags:
- tag1
- tag2
---

## Overview

These are the parts on the RadioLink hub schematic. Passives are omitted except where the value sets a current, as in the debug LED resistor. Prices are listed only where a vendor price was already chosen in component selection.

## Hub Bill of Materials

| **Part** | **Ref** | **Qty** | **Function** | **Unit cost** |
|:---|:---|:---:|:---|:---|
| PIC18F57Q43 Curiosity Nano | — | 1 | Hub microcontroller | — |
| UG-2864HSWEG01, 128x64 SSD1306 OLED | U1 | 1 | On-board graphics. Component selection chose the ER-OLED0.96-1.3W, the same controller class. | $2.49 |
| L7805CV | U4 | 1 | 9 V to 5 V | ~$1.08 |
| 3.3 V LDO, SOT-23-5 | U2 | 1 | OLED supply. The schematic does not name the orderable part. The block diagram rates this rail at 500 mA. | — |
| BSS138 | Q1, Q2 | 2 | I2C level shift between 5 V and 3.3 V | — |
| Red LED | D4 | 1 | Debug indicator. Series resistor R7 is 330 Ω. | — |
| 1N4148 | D1, D2, D3 | 3 | Small-signal diodes in the I2C level-shift network | — |
| 1 A fuse | F2 | 1 | Protects the 9 V input | — |
| Barrel jack | J1 | 1 | 9 V input | — |
| 8-pin socket | J4, J5, J6 | 3 | UART connectors to the other three boards | — |
| Pushbutton | SW1 | 1 | Local debug input on the hub. The user buttons are on board 2. | — |
| Jumper | JP1 | 1 | Disconnects power from the OLED | — |

The microphone, temperature sensor, user buttons, and speaker are not on this board.
