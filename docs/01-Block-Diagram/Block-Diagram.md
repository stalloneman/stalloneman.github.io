---
title: Individual Block Diagram
tags:
  - block-diagram
---

## Overview

This block diagram is the hub subsystem of RadioLink, Team 105's hub-and-spoke design. A Microchip PIC18F57Q43 Curiosity Nano sits at the center. A computer supplies 5 V over USB. An LM7805 provides a regulated 5 V rail rated for 1 A, and a separate 3.3 V regulator rated for 500 mA powers the display.

The microcontroller drives a 128x64 SSD1306 OLED (ER-OLED0.96-1.3W) over I2C. SDA is RB2 and SCL is RB1. The OLED side of that bus is 3.3 V, and the microcontroller side is 5 V. A red LED is driven from RA2 using PWM.

Three UART ports connect this hub to the other boards. Each link is 5 V and uses an RX/TX pair:

- Connector 1: RX on RC3, TX on RC2
- Connector 2: RX on RF1, TX on RF0
- Connector 3: RX on RA4, TX on RA3

These ports connect to the microphone board, the button and temperature board, and the speaker board. The microphone and button boards send data in. The hub shows temperature readings and the audio path on the OLED, and it sends the microphone signal out to the speaker.

## Block Diagram

![Team 105 hub block diagram](Individual Sultan Team 105 Block Diagram.drawio.png)

**Figure 1:** Hub block diagram for RadioLink, showing the PIC18F57Q43 Curiosity Nano, the OLED and I2C interface, the 5 V and 3.3 V supplies, the red LED, and three UART connectors to the other subsystems.
