# QL-EOS-S3-breakout

![Pinout guide)](https://raw.githubusercontent.com/Blinkinlabs/QL-EOS-S3-breakout/main/docs/img/board_revb.png)

A breadboard-friendly, low part count breakout board for the QuickLogic EOS-S3 ARM/FPGA IC.

The goals of this project are:

* Low-cost, minimum viable ARM+FPGA design that is breadboard compatable
* Footprint, power, UART pin compatibility with Teensy 3.2.
* All pins on Bank A placed in a group, because they can have their IO voltage set with a reference
* Bootstrap, SPI flash, and reset pins placed in non-breadboardable location to avoid inadvertant interference with application circuit
* Pins with multiple IO functions preferred over FPGA only pins
* Pins in understandable (ascending) order by FPGA IO number, when possible


See the [release PDF](https://raw.githubusercontent.com/Blinkinlabs/QL-EOS-S3-breakout/main/releases/2020-10-06_ql-eos-s3-breakout_RevB.pdf) for the schematic.
