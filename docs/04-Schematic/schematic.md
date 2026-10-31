---
title: Schematics
---

## Overview

This schematic is the hub subsystem of RadioLink for Team 105. It is centered on a PIC18F57Q43 Curiosity Nano. The hub reads the microphone board and the button and temperature board over UART, shows that information on the EastRising ER-OLED0.96-1.3W, sends the microphone signal to the speaker board, and drives a local debug LED.

Power comes from a 9 V barrel jack. A 1 A fuse feeds an ST L7805CV, which regulates that input to 5 V. A Microchip MCP1700-3302E/TO makes 3.3 V from that 5 V rail for the display. Two onsemi 2N7000G MOSFETs, Q1 and Q2, translate SDA and SCL between the 5 V microcontroller and the 3.3 V display. The display module uses an SSD1306 controller. Test points, a pushbutton, and the red LED provide debugging access on the microcontroller side. Three 8-pin connectors carry the UART links to the other subsystems.

The board is intended to use through-hole parts where that is practical. The OLED module is the exception.

> **TODO, ECAD not updated.** Figure 1, the PDF, and the KiCad zip are still the 2026-10-19 export. That export shows UG-2864HSWEG01 at U1, BSS138 at Q1 and Q2, and a 5-pin U2 with an enable pin. Do not treat the image as already containing the 2N7000G or the MCP1700-3302E/TO. The KiCad project was not edited, because the symbol pins and footprints cannot be swapped safely without checking ERC. These edits still have to be done in KiCad:
>
> - Replace the U1 symbol label with the ER-OLED0.96-1.3W module. Do not treat it as a UG-2864HSWEG01.
> - Replace Q1 and Q2 with onsemi 2N7000G, TO-92. Pin 1 is source, pin 2 is gate, pin 3 is drain. Source goes to the 3.3 V I2C side, drain goes to the 5 V I2C side, and gate goes to 3.3 V. Do not reuse the BSS138 footprint.
> - Replace U2 with MCP1700-3302E/TO, TO-92. Pin 1 is GND, pin 2 is VIN, pin 3 is VOUT. This part has no enable pin, so the EN net on the current symbol has to be removed rather than left floating.
> - Keep C1 and C2 at 10 µF only after checking that their ESR is between 0 Ω and 2.0 Ω.

![Hub Subsystem Schematic](Hub-Subsystem-Schematic.png)

**Figure 1:** Current hub schematic export. It still shows the previous OLED symbol, BSS138 level shifters, and the unlabeled 5-pin 3.3 V regulator. The intended parts are the ER-OLED0.96-1.3W, two 2N7000G devices, the L7805CV, and the MCP1700-3302E/TO.

## Function

RadioLink needs one board that can take the microphone and the button and temperature data, show it, and pass the microphone audio to the speaker. This schematic is that board.

The PIC18F57Q43 Curiosity Nano is the controller. Three UART connectors are the links to the other boards. One brings in the microphone, one brings in the pushbuttons and the temperature reading, and one carries the microphone signal out to the speaker. The connectors are logic-level RX and TX. They do not feed power to those boards, so the speaker amplifier is not a load on this schematic.

The ER-OLED0.96-1.3W is the interface the user sees. Board 2's buttons move through that screen. The module's SSD1306 logic is a 3.3 V interface, and the microcontroller I2C pins are 5 V, so Q1 and Q2 level-shift SDA and SCL. JP1 opens the display supply so the OLED can be powered down without shutting off the hub.

The 9 V barrel jack, the 1 A fuse, and the L7805CV make the 5 V rail for the microcontroller, the debug LED, and the UART logic. U2, the MCP1700-3302E/TO, makes the 3.3 V rail for the OLED from that 5 V rail. The red LED and SW1 are debug parts on this board. They are not the user controls. Those controls stay on board 2.

## Resources

A high-resolution PDF of the current, not-yet-updated schematic is available [*here*](Hub-Subsystem-Schematic.pdf).

The KiCad project for that same export is available as a [*ZIP archive*](Hub-Subsystem-KiCad-Project.zip).
