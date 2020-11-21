# Get Started


## Introduction
The QL-EOS-S3 board is a unique, low-cost microcontroller with a built-in FPGA.

## What you need
Hardware:

* [QL-EOS-S3 breakout board](https://github.com/Blinkinlabs/QL-EOS-S3-breakout)
* USB-C cable
* [3.3V FTDI cable](https://www.sparkfun.com/products/9717) (or other USB-serial converter)
* (optional) [Teensy 3.2](https://www.pjrc.com/store/teensy32.html), for restoring the SPI flash.
* (optional) ARM SWD adapter, such as the [Black magic probe](https://1bitsquared.com/products/black-magic-probe)

Software:

* ARM GCC toolchain, to compile code for the Cortex M4 processor
* Symbiflow toolchain, for generating FPGA bitstreams
* The QORC Software Development Kit
* Blinkinlabs example projects

## Installation

### Step 1: Install the toolchain
Follow the [toolchain setup](toolchain.md) instructions

### Step 2: Build an example project
Test a project that uses both the ARM and FPGA toolchains:

    cd ~/ql-eos-s3/qorc-sdk/bl_apps/bl_helloworldhw/GCC_Project
    make

### Step 3: Connect to the board
Connect your board to your computer using a USB cable, then connect an FTDI cable (technically optional):

![FTDI connection](img/ftdi_connection_revb.png)

Open your favorite serial terminal, and connect to the FTDI serial port with 115200,8N1 setting. Press the reset button on the board (the one closest to the SPI flash chip). The device should send a prompt:

    ##########################
    Blinkinlabs QL-EOS-S3 Breakout Bootloader
    SW Version: qorc-sdk/qf-apps/qf_bootloader(v2) (GCC)
    Nov 11 2020 00:29:45
    ##########################

As soon as you see the prompt, press and hold the user button (the one furthest from the SPI flash chip). The device will then go into bootloader mode, and send a prompt:

    User button pressed: switch to download mode
    FPGA Programmed
    Presss Reset button after flashing ..

If instead you see a message 'User button not pressed: proceeding to load application', just press reset, and try again.

### Step 4: Upload the example project
And try uploading it to the board:

    python3 ~/ql-eos-s3/TinyFPGA-Programmer-Application/tinyfpga-programmer-gui.py --m4app output/bin/bl_helloworldhw.bin --reset
    CLI mode
    ports =  ['/dev/ttyACM0 (QuickFeather)'] 1
    Using port  /dev/ttyACM0 (QuickFeather)
    Programming m4 application with  bl_helloworldhw.bin
    Erasing designated flash pages
    Erase  64.0 KiB ( 0xd8 ) at  0x80000
    Erase  32.0 KiB ( 0x52 ) at  0x90000
    Erase  4.0 KiB ( 0x20 ) at  0x98000
    Writing  binary
    Write  102172  bytes
    [XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX]
    Verifying  binary
    FastREAD 0x0B ( 102172 )
    [XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX]
    Success: read_back == data
    Writing metadata
    Erasing designated flash pages
    Erase  4.0 KiB ( 0x20 ) at  0x13000
    Writing  metadata
    Write  8  bytes
    [X]                                               ]
    Verifying  metadata
    FastREAD 0x0B ( 8 )
    [X]                                               ]
    Success: read_back == data
    Reset the device
    boot sent

On the serial terminal, the board should send progress updates:

    Addr: 0x00080000
    Erase 64 KBytes() .. done
    Addr: 0x00090000
    Erase 32 KBytes() .. done
    Addr: 0x00098000
    Erase 4 KBytes() .. done
    Addr: 0x00013000
    Erase 4 KBytes() .. done

And once it's finished, it will automatically restart:

    ##########################
    Blinkinlabs QL-EOS-S3 Breakout Bootloader
    SW Version: qorc-sdk/qf-apps/qf_bootloader(v2) (GCC)
    Nov 11 2020 00:29:45
    ##########################

    User button not pressed: proceeding to load application


    ##########################
    Quicklogic QuickFeather Standalone FPGA
    SW Version: qorc-sdk/qf_apps/qf_helloworldhw
    Nov 18 2020 18:01:17
    ##########################
