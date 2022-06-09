---
title: "Download and install Arm Compiler for Linux"
linkTitle: "Installing the Arm Compiler for Linux"
type: docs
weight: 1
description: >-
     This article describes how to download and install appropriate versions of the Arm Compiler for Linux
---

## Introduction

[Arm Compiler for Linux](https://developer.arm.com/Tools%20and%20Software/Arm%20Compiler%20for%20Linux) is tailored to the development of High Performance Computing (HPC) applications. Arm Compiler for Linux is a combination of Arm C/C++ Compiler (armclang), Arm Fortran Compiler (armflang), and Arm Performance Libraries (ArmPL).

## Pre-requisites
[Arm Compiler for Linux](https://developer.arm.com/Tools%20and%20Software/Arm%20Compiler%20for%20Linux) runs on 64-bit Arm hardware, it is not a cross-compiler.
You need 64-bit Arm hardware running one of the following Linux distributions:
  * Ubuntu (18.04 or 20.04)
  * Red Hat Enterprise Linux (RHEL7 or RHEL8) 
  * SUSE Linux Enterprise Server (SLES-15)

If any of the following tools are not already installed by your Linux distribution, you must install them before installing Arm Compiler for Linux:

Python (version 2.7 or later)
C Libraries:
  SUSE and RHEL: glibc-devel
  Ubuntu: libc6-dev
You must have at least 2 GB of free hard disk space to both download and unpack the Arm Compiler for Linux package. You must also have an additional 6 GB of free space to install the package.

## Download  {#download}

The Arm Compiler for Linux package for your Linux distribution can be downloaded [here](https://developer.arm.com/downloads/-/arm-compiler-for-linux).
The packages contain Arm C/C++/Fortran Compiler and Arm Performance Libraries.

Individual packages for just the Arm Performance Libraries can be also be downloaded from the [Product Downloads](https://developer.arm.com/downloads/-/arm-compiler-for-linux) section of the Arm website.

## Setting up product license {#license}

You do not require a license to use Arm Compiler for Linux.

## Installation {#install}

To install the Arm Compiler for Linux package on your 64-bit Linux Arm machine, follow the instructions [here](https://developer.arm.com/documentation/102621/0100/Install?lang=en).

## Get started {#start}

To get started with the [Arm Fortran Compiler](https://developer.arm.com/Tools%20and%20Software/Arm%20Fortran%20Compiler) and learn how to use it to compile Fortran source into an executable binary, follow the procedure [here](https://developer.arm.com/documentation/101380/2202/Get-started/Get-started-with-Arm-Fortran-Compiler).

To get started with the [Arm C/C++ Compiler](https://www.arm.com/products/development-tools/server-and-hpc/allinea-studio/cpp-compiler#:~:text=Arm%20C%2FC%2B%2B%20Compiler%20provides,C%2B%2B%2014%20and%20prior%20standards.&text=Our%20commercial%20compiler%20is%20based,by%20Arm%20for%20our%20architecture) and learn how to use it to compile C/C++ source into an executable binary, follow the procedure [here](https://developer.arm.com/documentation/101458/2202/Get-started/Get-started-with-Arm-C-C---Compiler).

To get started with the [Arm Performance Libraries](https://developer.arm.com/Tools%20and%20Software/Arm%20Performance%20Libraries) and learn how to select the optimal library for your system, follow the guide [here](https://developer.arm.com/documentation/102574/0100).

