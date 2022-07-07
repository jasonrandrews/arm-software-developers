---
title: "Getting Started with Arm Development Studio"
linkTitle: "Get Started with Arm Development Studio"
type: docs
weight: 1
description: >-
     This article describes how to set up and get started with Arm Development Studio. 
---

## Introduction

[Arm Development Studio](https://developer.arm.com/Tools%20and%20Software/Arm%20Development%20Studio) is the most comprehensive embedded C/C++ dedicated software development solution. It is used for validation of SoC debug through emulation, simulation, FPGA, and silicon bring-up design and verification stages. It has the earliest support for all Arm CPUs and interconnects.

## Pre-requisites

Arm Development Studio supports the following host platforms:

  * Windows 10
  * Red Hat Enterprise Linux 7 Workstation
  * Ubuntu Desktop Edition 18.04 LTS
  * Ubuntu Desktop Edition 20.04 LTS

Full host platform requirements are given in the [Getting Started Guide](https://developer.arm.com/documentation/101469/2022-0/Installing-and-configuring-Arm-Development-Studio/Hardware-and-host-platform-requirements)

## Download installer packages {#download}

You can download the Development Studio installer and examples suite from the [Product Downloads section]((https://developer.arm.com/downloads/-/arm-development-studio-downloads)) of the Arm website. Linux and Windows hosts are supported.

For Windows hosts, follow the installation instructions provided [here](https://developer.arm.com/documentation/101469/latest/Installing-and-configuring-Arm-Development-Studio/Installing-on-Windows).

For Linux hosts, follow the installation instructions provided [here](https://developer.arm.com/documentation/101469/latest/Installing-and-configuring-Arm-Development-Studio/Installing-on-Linux). Note also [additional Linux libraries](https://developer.arm.com/documentation/101469/latest/Installing-and-configuring-Arm-Development-Studio/Additional-Linux-libraries) are required.


## Setting up product license {#license}

Arm Development Studio is license managed. The licenses are enabled by a [Success Kit](https://www.arm.com/products/development-tools/success-kits).

Since Arm Development Studio version 2022.0 and 2022.a, Arm User-based licensing (UBL) is supported. To check if you have such a license enabled, use the
```console
armlm inspect
```
command. If a license is reported, then you are ready to use Arm Development Studio (and other Arm tools).

If no license is listed, you must [activate](https://developer.arm.com/documentation/102516/latest/Using-user-based-licensing) your license appropriately.

If using earlier versions or if no UBL license is available, you will need to set the environment variable `ARMLMD_LICENSE_FILE` is set to an appropriate license server.

Full license setup instructions are available [here](https://developer.arm.com/documentation/101469/latest/Installing-and-configuring-Arm-Development-Studio/Licensing-Arm-Development-Studio)

## Get started {#start}

To verify everything is installed correctly and to get started with your first project, follow the [Hello World Tutorial](https://developer.arm.com/documentation/101469/latest/Tutorials/Tutorial--Hello-World).

A number of [example projects](https://developer.arm.com/documentation/101469/latest/Projects-and-examples-in-Arm-Development-Studio/Examples-provided-with-Arm-Development-Studio) are also provided.

