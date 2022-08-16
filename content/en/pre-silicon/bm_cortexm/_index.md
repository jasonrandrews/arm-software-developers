---
title: "Get started Benchmarking Cortex-M processors"
linkTitle: "Cortex-M benchmarking"
type: docs
hide_summary: true
weight: 4
description: >
    Learn about how to get started benchmarking your Cortex-M code.
---
## Overview

The [Cortex-M](https://developer.arm.com/ip-products/processors/cortex-m/) series of low-latency, highly deterministic Arm processors are at the heart of many embedded and IoT applications. In this section we will learn how to perform benchmarking activities with a range of different Cortex-M targets, including virtual platforms.

## Learning Objectives 

By the end of this learning path, you will be able to use the following for benchmarking:
* SysTick timer
* DWT counters
* PMU events

## Pre-requisites

* [Arm Compiler for Embedded](https://developer.arm.com/Tools%20and%20Software/Arm%20Compiler%20for%20Embedded). If you are unsure how to access, see [this guide](compilers/install_armclang/).
* Appropriate Cortex-M target
    * Virtual platform, such as [Arm Fast Models](https://developer.arm.com/Tools%20and%20Software/Fast%20Models), [Fixed Virtual Platforms](https://developer.arm.com/Tools%20and%20Software/Fixed%20Virtual%20Platforms). or [Arm Virtual Hardware](https://developer.arm.com/Tools%20and%20Software/Arm%20Virtual%20Hardware).
    * Cortex-M hardware (eg [MPS2+](https://developer.arm.com/Tools%20and%20Software/MPS2%20Plus%20FPGA%20Prototyping%20Board)

## Sections

|          Type | Content       |
| ---           | ---           |
| How-To        | [Create a simple test example to perform profiling with](#) |
| How-To        | [Benchmarking with SysTick timer](#) |
| How-To        | [Benchmarking with DWT cycle counter](#) |
| How-To        | [Benchmarking with PMU events](#) |
| Optional How-To | [Benchmarking with Virtual Hardware using Iris API](#) |
| Check         | [Knowledge check and review](knowledgecheck) |

## References and Documentation

| Type          | Content             |
| ---           | ---                 |
| Documentation | [Armv8.1-M Performance Monitoring User Guide](https://developer.arm.com/documentation/arm051-799564642-251) |
| Documentation | [Iris User Guide](https://developer.arm.com/documentation/101196) |
| Reference     | [DWT (External)](https://mcuoneclipse.com/2017/01/30/cycle-counting-on-arm-cortex-m-with-dwt/) |

## Next Steps

[<-- Return to Learning Path](/pre-silicon/bm_cortexm/#sections)
