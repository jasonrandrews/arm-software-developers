---
title: "Installing GCC as a cross compiler on Linux"
linkTitle: "Installing GCC as a cross compiler on Linux"
type: docs
weight: 1
description: >-
     This article describes how to install GCC as a cross compiler on Linux.
---

## Introduction

The GCC toolchain is available on all Linux distributions. This section covers gcc and g++ as a cross compiler on Arm Linux distributions.

The cross gcc can be installed on x86 and aarch64 Linux machines.

## Download 

The Linux package manager will download the required files so there are no special download instructions.

## Installation {#install}

* Installing on Debian based distributions such as Ubuntu

Use the apt command to install software packages on any Debian based Linux distribution.

```console
sudo apt update
sudo apt install gcc-arm-none-eabi
```

* Installing on Red Hat / Fedora / Amazon Linux

These Linux distributions use yum as the package manager. 

To install the most common development tools use the commands below. If the machine has sudo you can use it or run yum as root.

```console
sudo yum update
sudo yum install arm-none-eabi-gcc-cs
```

If sudo is not availble become root and omit the sudo.

```console
yum update
yum install arm-none-eabi-gcc-cs
```

## Setting up product license {#license}

Arm GNU Toolchain is open source and freely available for use. No licenses need to be set up for use.

## Get started {#start}

To confirm the installation is complete run:

```console
arm-none-eabi-gcc --version
```

TBD: Need to provide an example, preferably with qemu to run it. 



