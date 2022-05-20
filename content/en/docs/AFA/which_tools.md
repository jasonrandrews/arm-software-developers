---
tags : ["software tools"]
title: "Which development tools are provided with Arm Flexible Access?"
linkTitle: "Which Tools are Supplied?"
date: 2022-05-16
description: >
   Arm Development Tools are provided as Arm Success Kits. This article will help understand the components provided therein.
---
## Arm Success Kits

Arm Flexible Access (AFA) provides development tools packaged as [Arm Success Kits](https://www.arm.com/products/development-tools/success-kits). These come in two forms:

- Software Success Kits (SSK)
- Hardware Success Kits (HSK)

The exact number of licenses for each Success Kit you will have will depend on your AFA program membership. Please contact your AFA administration team or Arm account manager if you need confirmation.

Software Success Kits contain all of the tools Arm provides for developing and running code for your target

- [Arm Development Studio](https://developer.arm.com/Tools%20and%20Software/Arm%20Development%20Studio) Gold Edition
  + includes [Arm Compiler for Embedded](https://developer.arm.com/Tools%20and%20Software/Arm%20Compiler%20for%20Embedded) and [Arm Compiler for Embedded FuSa](https://developer.arm.com/Tools%20and%20Software/Arm%20Compiler%20for%20Embedded%20FuSa)
- [Keil Microcontroller Development Kit](https://developer.arm.com/Tools%20and%20Software/Keil%20MDK) Professional Edition
- [Arm Fast Models](https://developer.arm.com/Tools%20and%20Software/Fast%20Models) run-time license
- [Arm Mobile Studio](https://developer.arm.com/Tools%20and%20Software/Arm%20Mobile%20Studio) Professional Edition
- [Arm Allinea Studio](https://developer.arm.com/Tools%20and%20Software/Arm%20Allinea%20Studio)

Hardware Success Kits are a super-set of Software Success Kits, adding tools for enabling architecture exploration, IP configuration, and system debug

- [Socrates](https://developer.arm.com/Tools%20and%20Software/Socrates)
- [AMBA Viz](https://developer.arm.com/Architectures/AMBA#Tools-and-Software)
- [Arm Fast Models](https://developer.arm.com/Tools%20and%20Software/Fast%20Models)
- Plus all SSK Components

**Note that as an AFA menber, you are also entitled to make use of [Arm IP Explorer](https://www.arm.com/products/ip-explorer). This is covered in a separate article.**

## Software development tools {#SDT}

The Software Success Kit contains 4 distinct suites of tools for software development. Each suite contains appropriate tools for a particular use case.

### Arm Development Studio

This is the most comprehensive embedded software development suite, supporting all Arm processors within the Arm Flexible Access program. It contains the industry leading Arm Compiler for Embedded, as well as a license for the Arm Compiler for Embedded FuSa (installed separately) for developers working in safety critical segments. This powerful tool can debug, trace, and profile the most advanced multi-core systems. Development Studio is hosted on Windows and Linux platforms.

### Keil Microcontroller Development Kit (MDK)

Keil MDK is a toolchain for developers working with Cortex-M microcontrollers. It is also provided with Arm Compiler for Embedded and enables Arm Compiler for Embedded FuSa. Designed around the CMSIS industry standard, it supports 9500+ microcontrollers. MDK is hosted on Windows platforms only.

### Arm Mobile Studio

Arm Mobile Studio is a suite of performance analysis tools that analyze the CPU activity, GPU activity and content metrics of your game as it runs on a non-rooted Android device. The Professional Edition enables users to integrate into a continuous integration (CI) development flow.

### Arm Allinea Studio

Arm Allinea Studio is a suite of tools for developing server and HPC applications on Arm-based platforms. It contains Arm-specific compilers (C/C++/Fortran) and libraries, plus debug and optimization tools.

## Fast Models {#fasstmodels}

Fast Models are accurate, flexible programmer's view models of Arm IP, allowing you to develop software such as drivers, firmware, OS and applications prior to silicon availability. Arm provides a selection of pre-built systems (Fixed Virtual Platforms (FVP)), as well as tooling (System Canvas) to enable you to build your own virtual platform, enabling software development prior to hardware availability.

The SSK license provides run-time licenses for Fast Models, enabling users with such a license to use the FVP or your own platform. The HSK license provides this capability as well as the ability to design and build your own platform.

## Hardware development tools {#HDT}

In addition to all the above SSK components, the HSK provides additional tooling for IP configuration and debug

### Socrates

The Socrates IP Tooling platform is an environment for exploring, configuring, and building Arm IP ready for integration into a System on Chip (SoC).

### AMBA Viz

AMBA Viz is a visualization application for viewing and interacting with hardware events and messages between components within a system, enabling faster, more intuitive debug capability.
