# Toolchain Setup

## Introduction
This is based on [Quickfeather getting started](https://github.com/QuickLogic-Corp/qorc-sdk#toolchain). There are instructions there for compiling from source.

## Prerequisites
Some prerequisites for a Debian / Ubuntu environment:

    sudo apt install build-essential
    sudo apt remove modemmanager
    sudo usermod -a -G dialout $USER

_Note: If you just added your user to dialout, log out and then back in again to apply the new membership_

Let's attempt to contain everything in a single directory:

    export INSTALL_DIR="$HOME/ql-eos-s3"
    mkdir $INSTALL_DIR
    cd $INSTALL_DIR

## ARM toolchain
First up, get ARM GCC:

    wget https://developer.arm.com/-/media/Files/downloads/gnu-rm/9-2020q2/gcc-arm-none-eabi-9-2020-q2-update-x86_64-linux.tar.bz2
    tar xvjf gcc-arm-none-eabi-9-2020-q2-update-x86_64-linux.tar.bz2 -C $INSTALL_DIR

    export PATH=$INSTALL_DIR/gcc-arm-none-eabi-9-2020-q2-update/bin/:$PATH

## FPGA toolchain
Then Symbiflow:

    wget 'https://github.com/QuickLogic-Corp/quicklogic-fpga-toolchain/releases/download/v1.3.0/Symbiflow_v1.3.0.gz.run'
    bash Symbiflow_v1.3.0.gz.run

    export PATH="$INSTALL_DIR/install/bin:$INSTALL_DIR/install/bin/python:$PATH"
    source "$INSTALL_DIR/conda/etc/profile.d/conda.sh"
    conda activate

And the TinyFPGA bootloader:

    git clone --recursive https://github.com/QuickLogic-Corp/TinyFPGA-Programmer-Application.git

    pip3 install pyserial
    pip3 install tinyfpgab

_Note: Make sure to activate conda in the previous step before using pip3 to install the python eggs_

## SDK
Now for the SDK and Blinkinlabs exmaples:

    git clone --recursive https://github.com/QuickLogic-Corp/qorc-sdk.git

    cd qorc-sdk
    git clone https://github.com/Blinkinlabs/bl_apps.git


# Default enviromnet
To make the tools available in your default environment, add the following to your .bashrc:

    # ARM gcc toolchain
    export PATH=$HOME/ql-eos-s3/gcc-arm-none-eabi-9-2020-q2-update/bin/:$PATH

    # FPGA toolchain for ql-eos-s3
    export INSTALL_DIR="$HOME/ql-eos-s3"
    export PATH="$HOME/ql-eos-s3/install/bin:$HOME/ql-eos-s3/install/bin/python:$PATH"
    source "$HOME/ql-eos-s3/conda/etc/profile.d/conda.sh"
    conda activate


