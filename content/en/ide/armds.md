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

Windows 7 SP1 Professional Edition
Windows 7 SP1 Enterprise Edition
Windows 10
Red Hat Enterprise Linux 7 Workstation
Ubuntu Desktop Edition 16.04 LTS
Ubuntu Desktop Edition 18.04 LTS

## Download installer packages {#download}

You can download the Development Studio installer and examples suite from the [Product Downloads section]((https://developer.arm.com/downloads/-/arm-development-studio-downloads)) of the Arm website. Linux and Windows hosts are supported.

For Linux hosts, follow the installation instructions provided [here](https://developer.arm.com/documentation/101469/2000/Installation/Installing-on-Linux).

For Windows hosts, follow the installation instructions provided [here](https://developer.arm.com/documentation/101469/2000/Installation/Installing-on-Windows).

## Setting up product license {#license}

All Arm Fast Models are license managed, and are enabled by a [Success Kit](https://www.arm.com/products/development-tools/success-kits).

Since Arm Development Studio version 2022.0 and 2022.a, Arm User-based licensing (UBL) is supported. To check if you have such a license enabled, use the `armlm inspect` command. If a license is reported, then you are ready to use Arm Development Studio (and other Arm tools).

If no license is listed, you must [activate](https://developer.arm.com/documentation/102516/latest/Using-user-based-licensing) your license appropriately.\
If no license is listed, you must [activate(internal link)](https://developer.arm.com/documentation-preview/102516/latest/Using-user-based-licensing) your license appropriately.

If using earlier versions or if no UBL license is available, you will need to set the environment variable `ARMLMD_LICENSE_FILE` is set to an appropriate license server. You may have set this at installation time via the GUI, follow the instructions provided [here](https://developer.arm.com/documentation/101469/2000/Licensing-Arm-Development-Studio?lang=en)

## Get started {#start}

To verify everything is installed correctly and to get started with your first project, follow the [Hello World Tutorial](https://developer.arm.com/documentation/101469/2000/Tutorials/Tutorial--Hello-World?lang=en)

