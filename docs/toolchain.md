# Toolchain setup

This is based on [Quickfeather getting started](https://github.com/QuickLogic-Corp/qorc-sdk#toolchain). There are instructions there for compiling from source.

Some prerequisites for a Debian / Ubuntu environment:

    sudo apt install build-essential
    sudo apt remove modemmanager
    sudo usermod -a -G dialout $USER

_Note: If you just added your user to dialout, log out and then back in again to apply the new membership_

Let's attempt to contain everything in a single directory:

    export INSTALL_DIR="$HOME/ql-eos-s3"
    mkdir $INSTALL_DIR
    cd $INSTALL_DIR

First up, get ARM GCC:

    wget https://developer.arm.com/-/media/Files/downloads/gnu-rm/9-2020q2/gcc-arm-none-eabi-9-2020-q2-update-x86_64-linux.tar.bz2
    tar xvjf gcc-arm-none-eabi-9-2020-q2-update-x86_64-linux.tar.bz2 -C $INSTALL_DIR

    export PATH=$INSTALL_DIR/gcc-arm-none-eabi-9-2020-q2-update/bin/:$PATH

Then the FPGA toolchain:

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

Now for the SDK and Blinkinlabs exmaples:

    git clone --recursive https://github.com/QuickLogic-Corp/qorc-sdk.git

    cd qorc-sdk
    git clone https://github.com/Blinkinlabs/bl_apps.git

Test a project that uses both the ARM and FPGA toolchains:

    cd $INSTALL_DIR/qorc-sdk/bl_apps/bl_helloworldhw/GCC_Project
    make

And try uploading it to the board:

_Note: First put your board in bootloader mode, by pressing the RESET button, followed by the USER button_

    python3 $INSTALL_DIR/TinyFPGA-Programmer-Application/tinyfpga-programmer-gui.py --m4app output/bin/bl_helloworldhw.bin --reset

If it's working, add the toolchain to your .bashrc:

    # ARM gcc toolchain
    export PATH=$HOME/ql-eos-s3/gcc-arm-none-eabi-9-2020-q2-update/bin/:$PATH

    # FPGA toolchain for ql-eos-s3
    export INSTALL_DIR="$HOME/ql-eos-s3"
    export PATH="$HOME/ql-eos-s3/install/bin:$HOME/ql-eos-s3/install/bin/python:$PATH"
    source "$HOME/ql-eos-s3/conda/etc/profile.d/conda.sh"
    conda activate


