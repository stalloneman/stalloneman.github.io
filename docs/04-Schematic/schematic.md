---
title: Schematics
---

## Overview

This schematic is the hub subsystem of RadioLink for Team 105. It is centered on a PIC18F57Q43 Curiosity Nano. The hub reads the microphone board and the button and temperature board over UART, shows that information on the EastRising ER-OLED0.96-1.3W, sends the microphone signal to the speaker board, and drives a local debug LED.

Power comes from a 9 V barrel jack. A 1 A fuse feeds an LM7805, which regulates that input to 5 V. A Microchip MCP1700-3302E/TO makes 3.3 V from that 5 V rail for the display. Two onsemi 2N7000 MOSFETs, Q1 and Q2, translate SDA and SCL between the 5 V microcontroller and the 3.3 V display. The display module uses an SSD1306 controller. Test points, a pushbutton, and the red LED provide debugging access on the microcontroller side. Three 8-pin connectors carry the UART links to the other subsystems.

The board is intended to use through-hole parts where that is practical. The OLED module and the 30-pin ZIF it plugs into are the exceptions. The connector is surface mount because a 0.5 mm, 30-pin ZIF does not have a practical through-hole version.

> **The published drawing is still the old plot.** Figure 1 and the PDF are the 2026-10-19 export. KiCad is not installed on this computer, so ERC was not run and a new plot was not made. The PCB file in the project was not updated. Open the schematic in KiCad, run ERC, then use Update PCB from Schematic.
>
> The schematic file inside the ZIP does have these changes:
>
> - U1 is the ER-OLED0.96-1.3W module. It stays in the BOM and is excluded from the board, because the module plugs in.
> - J7 is an EastRising ER-CON30HT-1, the 30-pin, 0.5 mm, top-contact ZIF that is soldered to the board. Each connector pin is placed on the same-numbered pin of U1, so it joins the net already wired there. No footprint is assigned. Use the EastRising land pattern and do not mirror pin 1. Pins 1 and 30 stay on the existing NC(GND) nets.
> - Q1 and Q2 are onsemi 2N7000. The symbol pin numbers are now pin 1 source, pin 2 gate, and pin 3 drain. The wires were not moved, so the source stays on the 3.3 V I2C side. The footprint is a project TO-92 at the usual 1.27 mm inline pitch. Confirm the flat face against the onsemi drawing before layout.
> - U2 is the MCP1700-3302E/TO. Pin 1 is GND, pin 2 is VIN, and pin 3 is VOUT. VOUT sits on the node that was called P4, which already connected to 3.3 V. The old OUT pin was a no-connect and was removed. The old EN pin was tied to GND, and that stub was removed because this regulator has no enable pin.
> - U4 is labeled LM7805. Its pins were already pin 1 input, pin 2 ground, and pin 3 output. No footprint is assigned.
> - C1 and C2 are still 10 µF. Check that their ESR is between 0 Ω and 2.0 Ω.

![Hub Subsystem Schematic](Hub-Subsystem-Schematic.png)

**Figure 1:** Previous hub schematic plot, from 2026-10-19. It still shows UG-2864HSWEG01, BSS138, and the 5-pin regulator. The schematic file in the ZIP is newer than this image.

## Function

RadioLink needs one board that can take the microphone and the button and temperature data, show it, and pass the microphone audio to the speaker. This schematic is that board.

The PIC18F57Q43 Curiosity Nano is the controller. Three UART connectors are the links to the other boards. One brings in the microphone, one brings in the pushbuttons and the temperature reading, and one carries the microphone signal out to the speaker. The connectors are logic-level RX and TX. They do not feed power to those boards, so the speaker amplifier is not a load on this schematic.

The ER-OLED0.96-1.3W is the interface the user sees. It plugs into J7, an EastRising ER-CON30HT-1 top-contact ZIF, which is the part soldered to the board. Board 2's buttons move through that screen. The module's SSD1306 logic is a 3.3 V interface, and the microcontroller I2C pins are 5 V, so Q1 and Q2 level-shift SDA and SCL. JP1 opens the display supply so the OLED can be powered down without shutting off the hub.

The 9 V barrel jack, the 1 A fuse, and the LM7805 make the 5 V rail for the microcontroller, the debug LED, and the UART logic. U2, the MCP1700-3302E/TO, makes the 3.3 V rail for the OLED from that 5 V rail. The red LED and SW1 are debug parts on this board. They are not the user controls. Those controls stay on board 2.

## Resources

A high-resolution PDF of the previous plot is available [*here*](Hub-Subsystem-Schematic.pdf). It does not include the part changes above.

The KiCad project, with the edited schematic and the unchanged PCB, is available as a [*ZIP archive*](Hub-Subsystem-KiCad-Project.zip).
