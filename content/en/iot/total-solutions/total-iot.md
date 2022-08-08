---
title: "Get started with Open-IoT-SDK and Arm Virtual Hardware"
linkTitle: "Get started with Open-IoT-SDK"
type: docs
toc_hide: true
hide_summary: true
weight: 30
description: >
    Learn about how to build and run the example software stacks provided as the Open-IoT-SDK.
---
## Overview
Developing IoT systems is incredibly complex. To fulfil the potential of IoT, we need to simplify and accelerate development for the entire value chain. [Arm Total Solutions for IoT](https://www.arm.com/solutions/iot/total-solutions-iot) is an industry first, bringing together specialized processing capabilities with standardized, secure software, and innovative approaches to tooling and development.

The [Arm Open-IoT-SDK](https://github.com/ARM-software/open-iot-sdk) provides a growing number of complete software stack examples for developers to use as the basis of their own IoT applications. The examples can be built and run on [Arm Virtual Hardware](https://avh.arm.com/).

## Pre-requisites

* [An Arm Virtual Hardware instance running in the cloud](/iot/aws/launch).

## Detailed Steps

### Clone the example repository

In your AVH terminal, clone the example repository, and navigate to the examples folder.
```console
git clone https://github.com/ARM-software/open-iot-sdk
cd open-iot-sdk/examples
```
Navigate to the desired example (`ats-keyword` in used here):
```console
cd ats-keyword
```
### Prepare build

For convenience a script `ats.sh` is provided to configure, build, and run all examples.

You must first synchronize git submodules, and apply required patches, which you can do with:
```console
./ats.sh bootstrap
```
Then install additional python dependencies required to run tests and sign binaries:
```console
sudo apt install python3.8-venv
python3.8 -m pip install imgtool cbor2
python3.9 -m pip install imgtool cffi intelhex cbor2 cbor pytest click
```
To make python user packages visible in the shell:
```console
export PATH=$PATH:/home/ubuntu/.local/bin
```
You are now ready to build the examples.

### Build an example

Use the `ats.sh` script to build the `Keyword Spotting` (`kws`) example:
```console
./ats.sh build kws
```

### Run the example on Arm Virtual Hardware

To then run the `kws` example on `Arm Virtual Hardware for Corstone-300`:
```console
./ats.sh run kws
```
and observe the output.
```
*** ML interface initialised
ML_HEARD_ON
INFO - For timestamp: 0.000000 (inference #: 0); label: on, score: 0.996094; threshold: 0.900000
INFO - For timestamp: 0.500000 (inference #: 1); label: on, score: 0.996094; threshold: 0.900000
INFO - For timestamp: 1.000000 (inference #: 2); label: on, score: 0.917969; threshold: 0.900000
ML_HEARD_OFF
INFO - For timestamp: 1.500000 (inference #: 3); label: off, score: 0.996094; threshold: 0.900000
...
```
Full details are given in the supplied `README.md`.

## Next Steps

Learn how to use [Arm Virtual Hardware in a CI/CD environment](/iot/cicd).

[<-- Return to Learning Path](/iot/total-solutions/#sections)
