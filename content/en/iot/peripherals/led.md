---
title: "Investigate example Virtual Peripheral implementation"
linkTitle: "Virtual Peripheral example"
type: docs
toc_hide: true
hide_summary: true
description: >
    Explore an example Python implementation of a Virtual Peripheral with Arm Virtual Hardware and Virtual IO.
---
## Overview

Learn how to create and integrate an LED peripheral with the Virtual IO (VIO) interface of Arm Virtual Hardware. An [example project](https://github.com/Arm-Examples/AVH-Virtual-Peripherals) is provided to help get started.

## Pre-requisites

* [An Arm Virtual Hardware instance running in the cloud](/iot/aws/launch)
* Some knowledge of [Python](https://www.python.org/) syntax.

## Detailed Instructions

### Prepare development environment

Launch an Arm Virtual Hardware (AVH) instance as [previously described](/iot/aws/launch).

The example used here makes use of the [Tkinter](https://docs.python.org/3/library/tkinter.html) Python interface to Tcl/Tk, and can be installed in the AVH instance with:
```console
sudo apt install python3-tk
```
### Clone the repository

In your AVH terminal, clone the example project repository, and navigate into the `leds_example` directory.
```console
git clone https://github.com/Arm-Examples/AVH-Virtual-Peripherals
cd AVH-Virtual-Peripherals/leds_example
```
### Build and run the example

A makefile is provided to build the example project. A `run.sh` script is provided to run the example.
```console
make
./run.sh
```
You can interact with the Virtual LEDs. If they are not displayed you may need to implement a [VNC connection](/iot/avh/launch/#vnc) to the AVH instance.

### Understand the example

The Virtual Hardware is launched with the `-V` option which specifies the python implementation of the peripheral. The python script(s) implement the [VIO Python interface](https://arm-software.github.io/AVH/main/simulation/html/group__arm__vio__py.html) to communicate with the Virtual Hardware application.

In the application, signals are passed via the [VIO API](https://arm-software.github.io/AVH/main/simulation/html/group__arm__vio__api.html) to/from the virtual peripheral.

## Next Steps

Learn about using the [Virtual Streaming Interface](#)

[<-- Return to Learning Path](/iot/peripherals/#sections)