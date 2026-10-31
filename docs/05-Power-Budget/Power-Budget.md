---
title: Power Budget
---

## Overview

This budget is for the RadioLink hub only. It covers the PIC18F57Q43 Curiosity Nano, the EastRising ER-OLED0.96-1.3W, the debug LED, the LM7805CT, and the MCP1700-3302E/TO. The microphone, button, and speaker boards are not included. Their UART links are logic-level signals, and those boards carry their own supplies.

The 9 V barrel jack feeds the LM7805CT. The 5 V rail feeds the PIC, the debug LED, and the MCP1700. The 3.3 V rail feeds the display. A linear regulator does not remove the load current. The MCP1700 input current is still a load on the 5 V rail, and that 5 V current is still a load on the 9 V input.

Currents below are datasheet limits or the allowances already used on this page. They are not lab measurements. The 25% margin is kept on each regulated rail. Quiescent current is included where the datasheet maximum is large enough to matter.

## Display current

The orderable display is the ER-OLED0.96-1.3W. SSD1306 is the controller on that module. EastRising Note 8 lists a maximum IBAT of 32.0 mA with the internal charge pump, VDD = 2.8 V, generated VCC = 7.25 V, and 100% of the pixels on. IDD maximum is 300 µA. Those two maxima add to:

32.0 mA + 0.3 mA = 32.3 mA

32.3 mA is the sum of those published maxima.

## Rails

![Hub power budget, loads and regulated rails](RadioLink-Power-Budget-Rails.png)

**Figure 1:** Loads on the 5 V rail and the 3.3 V rail, including the 25% margin.

![Hub power budget, 9 V source](RadioLink-Power-Budget-Source.png)

**Figure 2:** Current drawn from the 9 V barrel jack, including the 8 mA quiescent allowance.

### 3.3 V rail

The only 3.3 V load in this budget is the display, at 32.3 mA.

Margined current = 32.3 mA × 1.25 = 40.375 mA

The MCP1700-3302E/TO is rated for 250 mA when the output is 2.5 V or higher. Remaining capacity is 250 mA − 40.375 mA = 209.625 mA.

Load power and regulator loss at the 32.3 mA datasheet sum, not at the margin, are:

P_load = 3.3 V × 0.0323 A = 0.1066 W

P_MCP1700 = (5.0 V − 3.3 V) × 0.0323 A = 0.0549 W

P_input ≈ 5.0 V × 0.0323 A + 5.0 V × 4 µA = 0.1615 W

The 4 µA term is the MCP1700 maximum quiescent current. It does not change the milliamp total. TO-92 thermal resistance in the MCP1700 datasheet is 92 °C/W, so 0.0549 W is about a 5 °C rise.

### 5 V rail

| Load | Current |
| --- | ---: |
| PIC18F57Q43 Curiosity Nano allowance | 15 mA |
| Debug LED allowance, D4 with R7 = 330 Ω | 10 mA |
| MCP1700 input, equal to the 32.3 mA display current | 32.3 mA |
| Subtotal | 57.3 mA |
| After 25% margin | 71.625 mA |

The 15 mA PIC number is the operating allowance used for 5 V operation with UART, I2C, and PWM. The 10 mA LED allowance is for the Lite-On LTL-4293, whose typical forward voltage is 2.0 V at 10 mA, with R7 = 330 Ω.

The 5 V regulator is the LM7805CT. This budget uses a 7805-family estimate: 1.5 A output capability, 8 mA quiescent current, and 50 °C/W for the TO-220 package.

That 1.5 A rating leaves 1.5 A − 71.625 mA = 1.428 A. The 1 A fuse is on the 9 V input, not on the 5 V output.

At the margined 71.625 mA output current, using that 8 mA quiescent maximum:

P_LM7805 = (9 V − 5 V) × 0.071625 A + 9 V × 0.008 A = 0.359 W

At 50 °C/W the rise is about 18 °C. Output power is 5 V × 0.071625 A = 0.358 W. Input power is 9 V × (0.071625 A + 0.008 A) = 0.717 W. Efficiency is 0.358 / 0.717 = 50%. The LM7805 is appropriate in this estimate because the heat is small, not because a linear drop from 9 V to 5 V is efficient.

### 9 V input

Current from the barrel jack is the margined 5 V output current plus the 8 mA quiescent maximum:

71.625 mA + 8 mA = 79.625 mA

The fuse is 1 A, so the unused current is 1000 mA − 79.625 mA = 920.375 mA. The speaker amplifier stays on board 3. USB on the Curiosity Nano can power the microcontroller during programming, and that path is separate from this 9 V budget.

## Conclusions

The margined hub load is 71.625 mA on the 5 V rail and 40.375 mA on the 3.3 V rail. Against the 1.5 A 7805-family figure used above, and the MCP1700 250 mA rating, both loads are small. LM7805CT dissipation at the margined load is 0.359 W. MCP1700 dissipation at the 32.3 mA display sum is 0.0549 W. The 9 V input, limited by the 1 A fuse, still has 920 mA of spare current. The speaker amplifier stays on board 3.

## Resources

The spreadsheet is available as a [*ZIP archive*](RadioLink-Hub-Power-Budget.zip) and as an [*Excel file*](RadioLink-Hub-Power-Budget.xlsx).
