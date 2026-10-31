---
title: Schematics
---

## Overview

This schematic is the RadioLink hub for Team 105. The PIC18F57Q43 Curiosity Nano reads the microphone board and the button and temperature board over UART, shows the interface on the ER-OLED0.96-1.3W, and sends the microphone signal to the speaker board.

Power comes from a 9 V barrel jack, through a 1 A fuse, into an LM7805CT that makes the 5 V rail. An MCP1700-3302E/TO makes 3.3 V from that rail for the display. Two 2N7000 MOSFETs level-shift I2C between the 5 V microcontroller and the 3.3 V display. A debug LED and a debug button sit on this board. The user controls stay on board 2.

![Hub Subsystem Schematic](Hub-Subsystem-Schematic.png)

**Figure 1:** Hub subsystem schematic.

## Function

RadioLink needs one board that can collect the microphone and the button and temperature data, show it, and pass the microphone audio to the speaker. This schematic is that board.

Three UART connectors are the links to the other boards. One brings in the microphone, one brings in the pushbuttons and the temperature reading, and one carries the microphone signal out to the speaker. Those links are logic-level RX and TX. They do not power the other boards.

The ER-OLED0.96-1.3W is the interface the user sees. It plugs into an ER-CON30HT-1 top-contact ZIF. Board 2's buttons move through that screen. Q1 and Q2 level-shift SDA and SCL so the 5 V microcontroller can talk to the 3.3 V display. JP1 can open the display supply without shutting off the rest of the hub.

## Resources

A high-resolution PDF of this plot is available [*here*](Hub-Subsystem-Schematic.pdf).

The KiCad project is available as a [*ZIP archive*](Hub-Subsystem-KiCad-Project.zip).
