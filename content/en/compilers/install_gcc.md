---
title: "Download and install Arm GNU Toolchain"
linkTitle: "Installing the Arm GNU Toolchain"
type: docs
weight: 1
description: >-
     This article describes how to download and install appropriate versions of the GNU Toolchain for the Arm Architecure.
---

## Introduction

Arm GNU Toolchain is a community supported pre-built GNU compiler toolchain for Arm based CPUs.
There are many versions of the [Arm GNU Toolchain](https://developer.arm.com/Tools%20and%20Software/GNU%20Toolchain) available for use. In general, the latest version is recommended for use, as this will contain the latest optimization improvements, as well as support for the latest Arm IP. However there are reasons you may wish to use earlier compiler versions, when a specific compiler version is often mandated. 
## Download toolchain {#download}

Arm GNU Toolchain releases consists of cross toolchains for the following host operating systems:

GNU/Linux:
  * Available for x86_64 and AArch64 host architectures
  * Available for bare-metal and Linux targets

Windows:
  * Available for x86 host architecture only (compatible with x86_64)
  * Available for bare-metal and Linux targets

macOS:
  * Available for x86_64 host architecture only
  * Available for bare-metal targets only

Download the correct toolchain variant for your development needs from the Arm website [here](https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/downloads).

## Installation {#install}

* Installing executables on Linux *
Unpack the tarball to the install directory, like this:

    `$ cd ${install_dir} && tar xjf gcc-arm-none-eabi-_version_-linux.tar.bz2`

If you want to use gdb python build (arm-none-eabi-gdb-py), then
install python2.7.

For some Ubuntu releases, the toolchain can also be installed via
Launchpad PPA at https://launchpad.net/~team-gcc-arm-embedded/+archive/ubuntu/ppa.

* Installing executables on Mac OS X *
Unpack the tarball to the install directory, like this:

    `$ cd ${install_dir} && tar xjf gcc-arm-none-eabi-_version_-mac.tar.bz2`

* Installing executables on Windows *
Run the installer (gcc-arm-none-eabi-_version_-win32.exe) and follow the
instructions. The installer can also be run on the command line. When run on
the command-line, the following options can be set:
  - /S Run in silent mode
  - /P Adds the installation bin directory to the system PATH
  - /R Adds an InstallFolder registry entry for the install.

For example, to install the tools silently, amend users PATH and add registry
entry:

    > gcc-arm-none-eabi-_version_-win32.exe /S /P /R

The toolchain in Windows zip package is a backup to Windows installer for
those who cannot run the installer.  You must decompress the zip package
and then invoke it following instructions in the next section.

To use gdb python build (arm-none-eabi-gdb-py), you must install 32 bit
python2.7 irrespective of 32 or 64 bit Windows.  Please get the package from
https://www.python.org/download/.


## Setting up product license {#license}

Arm GNU Toolchain is open sourced and freely available for use. No licenses need to be set up for use.

## Get started {#start}

To check that the correct compiler version is being used, enter `arm-none-eabi-gcc -v`.\
To verify everything is working OK, you can get started by building the sample examples included in the toolchain installation at:

    `${install_dir}/gcc-arm-none-eabi-*/share/gcc-arm-none-eabi/samples`

