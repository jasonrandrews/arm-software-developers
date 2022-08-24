---
processors: [cortex-m]
software: [bare-metal]
title: "Create an example Cortex-M application"
linkTitle: "Create an example"
type: docs
weight: 1
hide_summary: true
description: >
    Create a simple example Cortex-M bare-metal application
---

## Learning Objectives 

By the end of this guide, you will be able to:

* Create a basic, but non-trivial, Cortex-M example, which we will use for further benchmarking examples.

## Pre-requisites

* [Arm Compiler for Embedded](https://developer.arm.com/Tools%20and%20Software/Arm%20Compiler%20for%20Embedded). If you are unsure how to access, see [this guide](compilers/install_armclang/).
* Appropriate Cortex-M target
    * Virtual platform, such as [Arm Fast Models](https://developer.arm.com/Tools%20and%20Software/Fast%20Models), [Fixed Virtual Platforms](https://developer.arm.com/Tools%20and%20Software/Fixed%20Virtual%20Platforms). or [Arm Virtual Hardware](https://developer.arm.com/Tools%20and%20Software/Arm%20Virtual%20Hardware).
    * Cortex-M hardware (eg [MPS2+](https://developer.arm.com/Tools%20and%20Software/MPS2%20Plus%20FPGA%20Prototyping%20Board)).

Arm Compiler for Embedded and the Fixed Virtual Platforms are installed as components of [Arm Development Studio](https://developer.arm.com/Tools%20and%20Software/Arm%20Development%20Studio) or [MDK Professional Edition](https://developer.arm.com/Tools%20and%20Software/Keil%20MDK).

## Detailed Steps

We will create a non-trivial application, making use of some key features of different Cortex-M processors, so that we shall be able to compare the relative performance in subsequent sections.

We shall compare:
 * [Cortex-M0+](https://developer.arm.com/Processors/Cortex-M0-Plus), the most energy efficient Arm processor.
 * [Cortex-M3](https://developer.arm.com/Processors/Cortex-M3), a general purpose processor.
 * [Cortex-M55](https://developer.arm.com/Processors/Cortex-M55), the first Armv8.1M processor, supporting the Helium instruction set.
  
### Create a simple source file

To do\
(note to self... see DS-Workspaces\bm_cortexm)

[<-- Return to Learning Path](pre-silicon/bm_cortexm)
