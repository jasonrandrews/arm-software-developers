---
title: "Download and install Arm GNU Toolchain"
linkTitle: "Installing the Arm GNU Toolchain"
type: docs
weight: 2
hide_summary: true
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

Download the correct toolchain variant for your development needs from the [Arm Developer website](https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/downloads).

## Installation {#install}

### Installing executables on Linux

Unpack the tarball to the install directory, and add the `bin` directory to `PATH`
```console
cd ${install_dir} && tar xjf gcc-arm-none-eabi-_version_-linux.tar.bz2
export PATH=${install_dir}/bin:$PATH
```
If you want to use `gdb python build` (`arm-none-eabi-gdb-py`), then
install `python2.7`.

For some Ubuntu releases, the toolchain can also be installed via
[Launchpad PPA](https://launchpad.net/~team-gcc-arm-embedded/+archive/ubuntu/ppa).

### Installing executables on Mac OS X
Unpack the tarball to the install directory
```console
cd ${install_dir} && tar xjf gcc-arm-none-eabi-_version_-mac.tar.bz2
```
Add `bin` directory to `$PATH` by editing the `/etc/paths` file with an appropriate editor, for example:
```console
sudo nano /etc/paths
```

### Installing executables on Windows
Double-click on the installer (e.g. `gcc-arm-_version_--mingw-w64-i686-arm-none-eabi.exe`) and follow on-screen instructions.

The installer can also be run on the command line. When run on
the command-line, the following options can be set:
  - `/S` Run in silent mode
  - `/P` Adds the installation `bin` directory to the system `PATH`
  - `/R` Adds Install Folder registry entry for the install.

For example, to install the tools silently, amend users `PATH` and add registry entry:
```console
gcc-arm-_version_--mingw-w64-i686-arm-none-eabi.exe /S /P /R
```

The zip package is a backup to Windows installer for those who cannot run the installer. You can unzip the package and then invoke it following instructions in the next section.

To use `gdb python build` (`arm-none-eabi-gdb-py`), you must install 32 bit
`python2.7` irrespective of 32 or 64 bit Windows. You can get the package from [here](https://www.python.org/download/).


## Setting up product license {#license}

Arm GNU Toolchain is open sourced and freely available for use. No licenses need to be set up for use.

To use the Arm GNU Toolchain in conjunction with [Arm Development Studio](https://developer.arm.com/Tools%20and%20Software/Arm%20Development%20Studio) you must [register the toolchain](https://developer.arm.com/documentation/101469/2022-0/Installing-and-configuring-Arm-Development-Studio/Register-a-compiler-toolchain).

## Get started {#start}

To verify the installation is correct enter:
```console
arm-none-eabi-gcc -v
```

Additional examples are included in the toolchain installation at:
```console
${install_dir}/_version_/share/gcc-arm-none-eabi/samples
```
