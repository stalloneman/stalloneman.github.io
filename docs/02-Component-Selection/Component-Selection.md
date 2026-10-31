---
title: Component Selection
---

The hub PCB is meant to be assembled, soldered, inspected, and repaired by hand. Through-hole packages are preferred wherever they are practical. The OLED module is an intentional exception, because that display assembly is not a discrete through-hole part.

Four parts were selected against that rule: the display module, the 9 V to 5 V regulator, the I2C level-shift MOSFETs, and the 5 V to 3.3 V regulator. SSD1306 is the controller inside the display. It is not the orderable module.

## OLED Display

**Requirements:** A readable graphic display for the hub UI, small enough for this board, with an I2C interface the PIC18F57Q43 can drive. Logic supply must work from the 3.3 V rail. The module may be a flex-connected assembly. It does not have to be through-hole.

SSD1306 names the controller IC. The orderable part is the EastRising module that uses that controller.

### Option 1: DLC-D1.54AGW#1

![DLC-D1.54AGW#1 OLED display](component-selection-assets/oled-dlc-1-54.png)

- $18.69 each
- [Link to product](https://www.digikey.com/en/products/detail/dlc-display-co-ltd/DLC-D1-54AGW-1/29925594)

| Pros | Cons |
| --- | --- |
| 128 x 64 resolution | 16-week lead time |
| Large 1.54-inch display | Requires 1 KB framebuffer |
| Common SSD1309 controller | Panel assembly, not a through-hole part |
| Open-source drivers available | Different controller from the selected module |

### Option 2: DLC-D2.23AGW#1

![DLC-D2.23AGW#1 OLED display](component-selection-assets/oled-dlc-2-23.jpeg)

- $25.40 each
- [Link to product](https://www.digikey.com/en/products/detail/dlc-display-co-ltd/DLC-D2-23AGW-1/26822637)

| Pros | Cons |
| --- | --- |
| Large 2.23-inch display | Fewer SSD1305 libraries available |
| Easy to read | Requires 12.5 V VCC |
| Only 512 bytes of PIC RAM for framebuffer | More expensive |
| | Only 128 x 32 resolution |
| | Panel assembly, not a through-hole part |

### Option 3: ER-OLED0.96-1.3W

![ER-OLED0.96-1.3W OLED display](component-selection-assets/oled-er-0-96.jpeg)

- $2.49 each
- [Link to product](https://www.buydisplay.com/128x64-oled-i2c-0-96-display-white-color-connector-fpc-ssd1306)
- [Series datasheet](../03-BOM/datasheets/ER-OLED0.96-1_Series_Datasheet.pdf)

This is an EastRising 0.96-inch, 128 x 64, white OLED module with a top-contact FPC. The controller on the module is an SSD1306. The module is not a breakout board.

EastRising lists VDD as 1.65 V to 3.3 V, typical 2.8 V. Logic-high is 0.8 x VDD. With the internal charge pump enabled, VBAT is specified as 3.5 V to 4.2 V. IDD is 180 µA typical and 300 µA maximum. With the charge pump generating VCC, IBAT at 100% of the pixels on is 25.6 mA typical and 32.0 mA maximum (datasheet Note 8: VDD = 2.8 V, generated VCC = 7.25 V). The framebuffer is 128 x 64 bits, which is 1 KB.

| Pros | Cons |
| --- | --- |
| SSD1306 controller, with I2C available on this module | 0.96-inch screen is small |
| 128 x 64 | FPC assembly, not through-hole |
| $2.49, and it was available to order | 1 KB framebuffer |
| Logic supply accepts 3.3 V | Charge-pump VBAT minimum in the datasheet is 3.5 V |

**Choice:** ER-OLED0.96-1.3W

**Rationale:** The hub UI only has to show temperature and audio status. A 128 x 64 SSD1306 module does that, costs $2.49, and does not have the 12- and 16-week lead times of the larger panels. Option 2 also needs 12.5 V, which this board does not have. The FPC module is the intentional exception to the through-hole preference. It mates with an EastRising ER-CON30HT-1, a 30-pin, 0.5 mm, top-contact ZIF.

## 9 V to 5 V Regulator

**Requirements:** Make a regulated 5 V rail from the 9 V barrel jack for the Curiosity Nano, the debug LED, and the current that the 3.3 V regulator draws. The package should be through-hole. The part must stay in regulation at 9 V and at the budgeted load, and the heat has to be acceptable without treating the regulator as an efficient converter.

The generic name "7805" is the 5 V family. The part selected for U4 is the Fairchild LM7805CT, a through-hole TO-220 regulator at $1.74.

### Option 1: L7805CV (STMicroelectronics)

![L7805CV voltage regulator](component-selection-assets/l7805cv.png)

- ~$1.08 each
- [Link to product](https://www.digikey.com/en/products/detail/stmicroelectronics/L7805CV/585964)
- [ST L78 datasheet](https://www.st.com/resource/en/datasheet/l78.pdf)

| Pros | Cons |
| --- | --- |
| Fixed 5 V, TO-220, through-hole | Linear regulator: the drop from 9 V to 5 V becomes heat |
| Output current up to 1.5 A | Quiescent current up to 8 mA at 25 °C |
| 9 V is inside the 7 V to 18 V test range used for the 5 V specification up to 1 A | Minimum load for regulation is 5 mA |
| Datasheet test circuit uses 0.33 µF in and 0.1 µF out, which is what the schematic already has (C9, C10) | Dropout is typically 2 V at 1 A and 25 °C, so it is not a low-dropout part |

### Option 2: MCP1702T-5002E/CB (Microchip)

![MCP1702T-5002E/CB voltage regulator](component-selection-assets/mcp1702.jpeg)

- ~$0.65 each
- [Link to product](https://www.digikey.com/en/products/detail/microchip-technology/MCP1702T-5002E-CB/1098473)

| Pros | Cons |
| --- | --- |
| Very low quiescent current | 250 mA maximum output |
| Good for battery operation | SOT-23, not through-hole |
| Accepts up to 13.2 V input | Less common than the 7805 family |
| High DigiKey stock | |

This option is a 5.0 V LDO. It is not the 3.3 V regulator selected later.

### Option 3: MC7805CDTRKG (onsemi)

![MC7805CDTRKG voltage regulator](component-selection-assets/mc7805.jpeg)

- ~$0.49 each
- [Link to product](https://www.digikey.com/en/products/detail/onsemi/MC7805CDTRKG/921037)

| Pros | Cons |
| --- | --- |
| Same 7805 family, 5 V output | Linear, so it also dissipates (9 V − 5 V) × Iout |
| Low cost | DPAK, not through-hole |
| Up to 1 A output | Harder to hand solder than TO-220 |

**Choice:** LM7805CT

- $1.74 each
- [Link to product](https://www.digikey.com/en/products/detail/fairchild-semiconductor/LM7805CT/12600247)

**Rationale:** The hub needs a through-hole 5 V regulator from the 9 V jack. The LM7805CT is available in TO-220 and is the part on the bill of materials. The L7805CV is ST's TO-220 part in the same family and was kept as the closest compared alternative. The MCP1702 was set aside because it is SOT-23 and its maximum output is 250 mA. The MC7805CDTRKG was set aside because it is DPAK. The budgeted 5 V current, after the 25% margin, is 71.625 mA. A 7805 is linear, so the drop from 9 V to 5 V becomes heat. That heat is small at this load, which is why a linear regulator is acceptable here.

## I2C Level-Shift MOSFET

**Requirements:** SDA and SCL have to cross between the 5 V PIC pins and the 3.3 V OLED pins. Two N-channel, through-hole MOSFETs are used, one for each line.

**Choice:** two onsemi 2N7000, Q1 and Q2

![onsemi 2N7000](component-selection-assets/2n7000.png)

- $0.65 each
- [2N7000 on DigiKey](https://www.digikey.com/en/products/detail/onsemi/2N7000/244278)
- [onsemi 2N7000 datasheet](../03-BOM/datasheets/2N7000.pdf)

**Rationale:** The 2N7000 is inexpensive, widely stocked, and commonly used for this kind of I2C level shift. One device is used on SDA and one on SCL.

## 5 V to 3.3 V Regulator

**Requirements:** A second regulator has to make 3.3 V from the 5 V rail for the OLED. It needs a fixed 3.3 V output and a through-hole package. The display load used in the power budget is 32.3 mA.

**Choice:** MCP1700-3302E/TO

![MCP1700-3302E/TO](component-selection-assets/mcp1700-3302e-to.png)

- $0.50 each
- Fixed 3.3 V, TO-92, 250 mA
- [MCP1700-3302E/TO on DigiKey](https://www.digikey.com/en/products/detail/microchip-technology/MCP1700-3302E-TO/652680)
- [Microchip MCP1700 datasheet](../03-BOM/datasheets/MCP1700.pdf)

**Rationale:** The MCP1700-3302E/TO is inexpensive, widely stocked, and a common through-hole 3.3 V regulator. It supplies the OLED from the 5 V rail.

## MCC Configuration

The hub uses the PIC18F57Q43 on the Curiosity Nano. The clock is the internal HFINTOSC. There is no external crystal on the schematic. Peripheral pin select maps the digital pins below.

| Function | Peripheral | Pins |
| --- | --- | --- |
| System clock | HFINTOSC | Internal |
| OLED I2C, after the 2N7000 shifters | I2C | SDA on RB2, SCL on RB1 |
| Debug LED | PWM | RA2 |
| UART connector 1 | UART | TX on RC2, RX on RC3 |
| UART connector 2 | UART | TX on RF0, RX on RF1 |
| UART connector 3 | UART | TX on RA3, RX on RA4 |
| Debug button | GPIO input | SW1 |

The three UART ports link this hub to the microphone board, the button and temperature board, and the speaker board. I2C is shifted from 5 V at the microcontroller to 3.3 V at the OLED by Q1 and Q2. SW1 is the debug button on this board. The user buttons are on board 2.
