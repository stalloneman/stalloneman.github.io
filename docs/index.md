---
title: Khushamadeed!
tags:
- tag1
- tag2
---
<center>
<font size= "6">Sultan Haidar Ali Datasheet</font><br>
as part of<br>
<font size= "8"> RadioLink</font><br>
for<br>
<font size= "5"> Team 105 </font><br>

**Submission: 10, 26, 2026**
</center>

## Introduction

This datasheet documents the hub subsystem of RadioLink, Team 105's embedded project. It is written so the design can be reviewed on its own, without the team report open beside it.

### Project Summary

RadioLink is organized as a hub-and-spoke system. Sensor boards send measurements to a central hub, the hub combines that information and shows it on an OLED, and the hub sends commands out to the actuators on the other boards. This site covers that hub: the PIC18F57Q43 Curiosity Nano, the display, the power supplies, and the UART links to the rest of the team.

### My Contribution

My work on RadioLink has centered on concept ideation, user-needs benchmarking, and the hub itself. I defined how the boards share information, then designed the subsystem that receives sensor data from the other boards, combines it, presents it with a custom interface on the OLED, and sends the resulting signals to the actuators on those boards.

- [Block Diagram](01-Block-Diagram/Block-Diagram.md)
- [Component Selection](02-Component-Selection/Component-Selection.md)
- [Bill of Materials](03-BOM/BOM.md)
- [Schematic](04-Schematic/schematic.md)
- [Power Budget](05-Power-Budget/Power-Budget.md)
