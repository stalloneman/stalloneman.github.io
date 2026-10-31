---
title: Individual Block Diagram
tags:
  - block-diagram
---

## Overview

This block diagram is the hub of RadioLink, Team 105's hub-and-spoke design. A PIC18F57Q43 Curiosity Nano sits at the center. The 9 V input is regulated to 5 V by an LM7805CT. An MCP1700-3302E/TO makes 3.3 V from that rail for the EastRising ER-OLED0.96-1.3W. I2C between the microcontroller and the display is level-shifted with 2N7000 MOSFETs. A debug LED is driven from RA2.

Three UART ports connect the hub to the other boards. Each link is 5 V and uses an RX/TX pair:

- Connector 1: RX on RC3, TX on RC2
- Connector 2: RX on RF1, TX on RF0
- Connector 3: RX on RA4, TX on RA3

The microphone board and the button and temperature board send data in. The hub shows that information on the OLED, which is navigated with board 2's buttons, and it sends the microphone signal out to the speaker board.

## Block Diagram

![Team 105 hub block diagram](Individual Sultan Team 105 Block Diagram.drawio.png)

**Figure 1:** Hub block diagram for RadioLink.

## Resources

The exported block diagram is available as a [*ZIP archive*](Hub-Block-Diagram-Source.zip).
