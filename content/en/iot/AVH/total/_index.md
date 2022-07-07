---
title: "Get started with Arm Total Solutions for IoT"
linkTitle: "Get started with Arm Total Solutions for IoT"
type: docs
weight: 30
description: >
    Learn about Arm Total Solutions for the Internet of Things, and how to build and run the example software stacks
---
Developing IoT systems is incredibly complex. To fulfil the potential of IoT, we need to simplify and accelerate development for the entire value chain. [Arm Total Solutions for IoT](https://www.arm.com/solutions/iot/total-solutions-iot) is an industry first, bringing together specialized processing capabilities with standardized, secure software, and innovative approaches to tooling and development.

The [Arm Open-IoT-SDK](https://github.com/ARM-software/open-iot-sdk) provides a growing number of complete software stack examples for developers to use as the basis of their own IoT applications. The examples can be built and run on [Arm Virtual Hardware](https://avh.arm.com/).

## Get started

To get started, launch an Arm Virtual Hardware [session](https://avh.arm.com) on AWS. This invokes a cloud based instance of Ubuntu Linux with all necessary Arm toolc pre-installed. Alternatively you can use your own local environment. For tooling installation instructions, see [Getting Started](/successkits/install)

Clone the Open-IoT-SDK repository, and navigate to the examples directory
```console
git clone https://github.com/ARM-software/open-iot-sdk
cd open-iot-sdk/examples
```

Navigate to the desired example folder (`ats-keyword` in used here):
```console
cd ats-keyword
```

and you will find `ats.sh` script to build and run the examples. You should first synchronize git submodules, and apply required patches, which you can do with:
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

You are now ready to build the examples. To build the `blinky` example:
```console
./ats.sh build blinky
```

To then run the built example on the supplied `Arm Virtual Hardware for Corstone-300`:
```console
./ats.sh run blinky
```

Full details are given in the supplied `readme` for the example.