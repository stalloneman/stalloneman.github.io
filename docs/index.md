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

This datasheet documents the hub subsystem of RadioLink, Team 105's embedded project.

### Project Summary

RadioLink is a hub-and-spoke system, and this board is the hub. It has an on-board OLED for graphics, a debug LED, and three UART ports. Board 1 carries the microphone, board 2 carries the pushbuttons and a temperature sensor, and board 3 carries the speaker. The microphone and button boards send their data to the hub. The hub shows a custom interface on the OLED, which is navigated with board 2's buttons, and it plays the microphone signal through the speaker.

### My Contribution

My work on RadioLink has centered on concept ideation, user-needs benchmarking, and the hub itself. The hub receives the microphone and temperature data, presents it on a custom OLED interface that is navigated with the pushbuttons, and sends the microphone signal to the speaker.

- [Block Diagram](01-Block-Diagram/Block-Diagram.md)
- [Component Selection](02-Component-Selection/Component-Selection.md)
- [Bill of Materials](03-BOM/BOM.md)
- [Schematic](04-Schematic/schematic.md)
- [Power Budget](05-Power-Budget/Power-Budget.md)
