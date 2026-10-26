---
title: Schematics
---

## Overview

This schematic is the hub subsystem of RadioLink for Team 105. It is centered on a PIC18F57Q43 Curiosity Nano. The hub reads the microphone board and the button and temperature board over UART, shows that information on a 128x64 SSD1306 OLED, sends the microphone signal to the speaker board, and drives a local debug LED.

Power comes from a 9 V barrel jack. A 1 A fuse feeds an LM7805, which regulates that input to 5 V for the microcontroller and the UART connectors. A separate 3.3 V supply powers the OLED. BSS138 level shifters translate the I2C signals between the 5 V microcontroller and the 3.3 V display. Test points, a pushbutton, and the red LED provide debugging access on the microcontroller side. Three 8-pin connectors carry the UART links to the other subsystems.

![Hub Subsystem Schematic](Hub-Subsystem-Schematic.png)

**Figure 1:** Hub subsystem schematic for RadioLink, showing the microcontroller and debug circuitry, the OLED and I2C interface, 9 V input and 5 V regulation, and the three UART connectors.

## Function

RadioLink needs one board that can take the microphone and the button and temperature data, show it, and pass the microphone audio to the speaker. This schematic is that board.

The PIC18F57Q43 Curiosity Nano is the controller. Three UART connectors are the links to the other boards. One brings in the microphone, one brings in the pushbuttons and the temperature reading, and one carries the microphone signal out to the speaker. The connectors are logic-level RX and TX. They do not feed power to those boards, so the speaker amplifier is not a load on this schematic.

The 128x64 OLED is the interface the user sees. Board 2's buttons move through that screen. The display is a 3.3 V part, and the microcontroller I2C pins are 5 V, so Q1 and Q2 (BSS138) level-shift SDA and SCL. JP1 opens the display supply so the OLED can be powered down without shutting off the hub.

The 9 V barrel jack, the 1 A fuse, and the LM7805 make the 5 V rail for the microcontroller, the debug LED, and the UART logic. U2 makes the 3.3 V rail for the OLED. The red LED and SW1 are debug parts on this board. They are not the user controls. Those controls stay on board 2.

## Resources

A high-resolution PDF of the schematic is available [*here*](Hub-Subsystem-Schematic.pdf).

The complete KiCad project is available as a [*ZIP archive*](Hub-Subsystem-KiCad-Project.zip).
