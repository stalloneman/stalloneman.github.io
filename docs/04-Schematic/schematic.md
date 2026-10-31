---
title: Schematics
---

## Overview

This schematic is the hub subsystem of RadioLink for Team 105. It is centered on a PIC18F57Q43 Curiosity Nano. The hub reads the microphone board and the button and temperature board over UART, shows that information on the EastRising ER-OLED0.96-1.3W, sends the microphone signal to the speaker board, and drives a local debug LED.

Power comes from a 9 V barrel jack. A 1 A fuse feeds an LM7805, which regulates that input to 5 V. A Microchip MCP1700-3302E/TO makes 3.3 V from that 5 V rail for the display. Two onsemi 2N7000 MOSFETs, Q1 and Q2, translate SDA and SCL between the 5 V microcontroller and the 3.3 V display. The display module uses an SSD1306 controller. Test points, a pushbutton, and the red LED provide debugging access on the microcontroller side. Three 8-pin connectors carry the UART links to the other subsystems.

The board is intended to use through-hole parts where that is practical. The OLED module and the 30-pin ZIF it plugs into are the exceptions. The connector is surface mount because a 0.5 mm, 30-pin ZIF does not have a practical through-hole version.

Figure 1 and the PDF are the schematic plot exported on 2026-10-30. The title block on that sheet still prints 2026-10-19. ERC was not run from this computer, and the PCB file was not updated from the schematic.

This plot shows U1 as the ER-OLED0.96-1.3W, Q1 and Q2 as 2N7000, U2 as the MCP1700-3302E/TO, and U4 as the LM7805. It does not show a placed ER-CON30HT-1. That top-contact ZIF is still the connector the module plugs into, and it is listed on the bill of materials. C1 and C2 are still 10 µF. Check that their ESR is between 0 Ω and 2.0 Ω.

![Hub Subsystem Schematic](Hub-Subsystem-Schematic.png)

**Figure 1:** Hub schematic exported 2026-10-30. U1 is the ER-OLED0.96-1.3W, Q1 and Q2 are 2N7000, U2 is the MCP1700-3302E/TO, and U4 is the LM7805. The title block date still reads 2026-10-19.

## Function

RadioLink needs one board that can take the microphone and the button and temperature data, show it, and pass the microphone audio to the speaker. This schematic is that board.

The PIC18F57Q43 Curiosity Nano is the controller. Three UART connectors are the links to the other boards. One brings in the microphone, one brings in the pushbuttons and the temperature reading, and one carries the microphone signal out to the speaker. The connectors are logic-level RX and TX. They do not feed power to those boards, so the speaker amplifier is not a load on this schematic.

The ER-OLED0.96-1.3W is the interface the user sees. The module is meant to plug into an EastRising ER-CON30HT-1 top-contact ZIF. That connector is not drawn on this plot. Board 2's buttons move through that screen. The module's SSD1306 logic is a 3.3 V interface, and the microcontroller I2C pins are 5 V, so Q1 and Q2 level-shift SDA and SCL. JP1 opens the display supply so the OLED can be powered down without shutting off the hub.

The 9 V barrel jack, the 1 A fuse, and the LM7805 make the 5 V rail for the microcontroller, the debug LED, and the UART logic. U2, the MCP1700-3302E/TO, makes the 3.3 V rail for the OLED from that 5 V rail. The red LED and SW1 are debug parts on this board. They are not the user controls. Those controls stay on board 2.

## Resources

A high-resolution PDF of this plot is available [*here*](Hub-Subsystem-Schematic.pdf).

The KiCad project, with the edited schematic and the unchanged PCB, is available as a [*ZIP archive*](Hub-Subsystem-KiCad-Project.zip).
