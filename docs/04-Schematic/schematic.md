---
title: Schematics
---

## Overview

This schematic is the hub subsystem of RadioLink for Team 105. It is centered on a PIC18F57Q43 Curiosity Nano. The hub reads the other boards over UART, shows the combined information on a 128x64 SSD1306 OLED, and drives a local debug LED.

Power comes from a 9 V barrel jack. A 1 A fuse feeds an LM7805, which regulates that input to 5 V for the microcontroller and the UART connectors. A separate 3.3 V supply powers the OLED. BSS138 level shifters translate the I2C signals between the 5 V microcontroller and the 3.3 V display. Test points, a pushbutton, and the red LED provide debugging access on the microcontroller side. Three 8-pin connectors carry the UART links to the other subsystems.

![Hub Subsystem Schematic](Hub-Subsystem-Schematic.png)

**Figure 1:** Hub subsystem schematic for RadioLink, showing the microcontroller and debug circuitry, the OLED and I2C interface, 9 V input and 5 V regulation, and the three UART connectors.

## Resources

A high-resolution PDF of the schematic is available [*here*](Hub-Subsystem-Schematic.pdf).

The complete KiCad project is available as a [*ZIP archive*](Hub-Subsystem-KiCad-Project.zip).
