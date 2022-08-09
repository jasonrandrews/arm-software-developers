---
title: "Build and run example project in an Arm Virtual Hardware session in the cloud"
linkTitle: "Build example project"
type: docs
weight: 2
hide_summary: true
description: >
    How to build and run a microspeech example in an Arm Virtual Hardware session in the cloud.
---
## Overview

To help users get started, a [Microspeech reference example](https://github.com/ARM-software/AVH-TFLmicrospeech) developed with [Keil MDK](https://www2.keil.com/mdk5) is available for users to build and run with Arm Virtual Hardware. All necessary software to build and execute the example are provided. For a thorough understanding of the example, see the associated `README.md` documentation.

## Pre-requisites

* [An Arm Virtual Hardware instance running in the cloud](/iot/aws/launch)

## Detailed Steps

### Clone the example repository

In your AVH terminal, clone the example repository, and navigate to the example folder.
```console
git clone https://github.com/ARM-software/AVH-TFLmicrospeech
cd AVH-TFLmicrospeech/Platform_FVP_Corstone_SSE-300_Ethos-U55
```

### Build the example

Rebuild the project, which you can do from the command line with:
```console
cbuild.sh microspeech.Example.cprj
```
The build will take some time to complete.

### Run the example on Arm Virtual Hardware

A script is provided to launch the Corstone-300 Virtual Hardware Target:
```console
./run_example.sh
```
You will see output similar to the following, and execution will complete.
```
telnetterminal0: Listening for serial connection on port 5000
telnetterminal1: Listening for serial connection on port 5001
telnetterminal2: Listening for serial connection on port 5002
telnetterminal5: Listening for serial connection on port 5003

    Ethos-U rev 136b7d75 --- Nov 25 2021 12:44:08
    (C) COPYRIGHT 2019-2021 Arm Limited
    ALL RIGHTS RESERVED

Heard yes (146) @1000ms
Heard no (145) @5600ms
Heard yes (143) @9100ms
Heard no (145) @13600ms
Heard yes (143) @17100ms
Heard no (145) @21600ms

Info: Simulation is stopping. Reason: Simulated time has been exceeded.

Info: /OSCI/SystemC: Simulation stopped by user.
[warning ][main@0][01 ns] Simulation stopped by user

--- cpu_core statistics: ------------------------------------------------------
Simulated time                          : 24.000000s
User time                               : 3.834549s
System time                             : 0.022307s
Wall time                               : 4.265401s
Performance index                       : 5.63
cpu_core.cpu0                           : 102.31 MIPS (   394585852 Inst)
-------------------------------------------------------------------------------
```
## Other resources

Further [software examples](https://arm-software.github.io/AVH/main/examples/html/index.html) for use with Arm Virtual Hardware are being developed.

## Next Steps

* (Optional) You can learn how to [connect Arm Development Studio debugger to your AVH instance in the cloud](/iot/avh/arm-development-studio).

[<-- Return to Learning Path](/iot/avh/#sections)
