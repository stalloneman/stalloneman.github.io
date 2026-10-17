---
title: Component Selection
---

## OLED Display

**Requirements:** Readable, compact, and easy to implement.

### Option 1: DLC-D1.54AGW#1

![DLC-D1.54AGW#1 OLED display](component-selection-assets/oled-dlc-1-54.png)

- $18.69 each
- [Link to product](https://www.digikey.com/en/products/detail/dlc-display-co-ltd/DLC-D1-54AGW-1/29925594)

| Pros | Cons |
| --- | --- |
| 128 x 64 resolution | 16-week lead time |
| Large 1.54-inch display | Requires 1 KB framebuffer |
| Common SSD1309 controller | |
| Open-source drivers available | |

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

### Option 3: ER-OLED0.96-1.3W

![ER-OLED0.96-1.3W OLED display](component-selection-assets/oled-er-0-96.jpeg)

- $2.49 each
- [Link to product](https://www.buydisplay.com/128x64-oled-i2c-0-96-display-white-color-connector-fpc-ssd1306)

| Pros | Cons |
| --- | --- |
| Common SSD1306 controller | Small 0.96-inch display |
| Many libraries and examples available | Requires 1 KB framebuffer |
| Low cost | |
| Easy to implement | |
| Fast shipping | |

**Choice:** Option 3: ER-OLED0.96-1.3W

**Rationale:** Option 3 is inexpensive, easy to implement, and available quickly. The SSD1306 is well documented and has many open-source libraries, making PIC integration easier. The 0.96-inch display is small, but it should be readable for a handheld device. Options 1 and 2 have lead times of 16 and 12 weeks.

## Voltage Regulator

**Requirements:** Convert a 9 V battery supply to 5 V for the microphone and speaker circuits.

### Option 1: L7805CV (STMicroelectronics)

![L7805CV voltage regulator](component-selection-assets/l7805cv.jpeg)

- ~$1.08 each
- [Link to product](https://www.digikey.com/en/products/detail/stmicroelectronics/L7805CV/585964)

| Pros | Cons |
| --- | --- |
| Widely used 7805 regulator | Wastes power as heat |
| Extensive documentation | Large TO-220 package |
| High DigiKey stock | |
| 5 V output from 9 V input | |
| Up to 1.5 A output | |
| Easy to prototype | |

### Option 2: MCP1702T-5002E/CB (Microchip)

![MCP1702T-5002E/CB voltage regulator](component-selection-assets/mcp1702.jpeg)

- ~$0.65 each
- [Link to product](https://www.digikey.com/en/products/detail/microchip-technology/MCP1702T-5002E-CB/1098473)

| Pros | Cons |
| --- | --- |
| Very low quiescent current | 250 mA maximum output |
| Good for battery operation | Harder to breadboard or hand solder |
| Accepts up to 13.2 V input | Less common than the 7805 family |
| High DigiKey stock | |
| Small SOT-23 package | |

### Option 3: MC7805CDTRKG (onsemi)

![MC7805CDTRKG voltage regulator](component-selection-assets/mc7805.jpeg)

- ~$0.49 each
- [Link to product](https://www.digikey.com/en/products/detail/onsemi/MC7805CDTRKG/921037)

| Pros | Cons |
| --- | --- |
| Widely used 7805 family | Wastes power as heat |
| Low cost | Harder to breadboard |
| Good DigiKey availability | Higher quiescent current than MCP1702 |
| Up to 1 A output | |
| Compact DPAK package | |

**Choice:** Option 1: L7805CV

**Rationale:** Option 1 is widely used, well documented, and readily available. Its 1.5 A output also provides plenty of current for the circuit. The through-hole package makes it easy to prototype.
