---
title: "Using the Arm ML Evaluation Kit with Arm Virtual Hardware"
linkTitle: "ML Evaluation Kit with AVH"
type: docs
weight: 1
hide_summary: true
weight: 30
description: >
    Learn about the ML Evaluation Kit and how to use it with Corstone-300 and Arm Virtual Hardware
---
## Overview
Developers have access to an easy to use platform to develop powerful embedded and IoT applications, making use of the latest Machine Learning (ML) technology from Arm. [Arm Virtual Hardware](https://www.arm.com/en/products/development-tools/simulation/virtual-hardware) provides a growing number of platforms to get started with software development.

In parallel, Arm has developed the [ML Evaluation Kit](https://review.mlplatform.org/plugins/gitiles/ml/ethos-u/ml-embedded-evaluation-kit), which includes ready-to-use ML applications. These allow you to investigate the embedded software stack and evaluate performance of the networks running on the Cortex-M55 and Ethos-U55 processors.

The Virtual Hardware is also a digital twin of the [MPS3](https://www.arm.com/products/development-tools/development-boards/mps3) FPGA image ([Application Note 547](https://developer.arm.com/downloads/-/download-fpga-images)). This enables easy code migration from a virtual to a physical platform, allowing for real-world trials of your application.

Full instructions are provided in the evaluation kit [documentation](https://review.mlplatform.org/plugins/gitiles/ml/ethos-u/ml-embedded-evaluation-kit/+/HEAD/docs/quick_start.md)

## Pre-requisites

* [An Arm Virtual Hardware instance running in the cloud](/iot/aws/launch)

## Detailed Steps

### Clone the Evaluation kit repository:

In your Arm Virtual Hardware terminal, clone the ML Evaluation Kit repository, and navigate into its directory.
```console
git clone "https://review.mlplatform.org/ml/ethos-u/ml-embedded-evaluation-kit"
cd ml-embedded-evaluation-kit
```

### Resolve external dependencies and prepare build environment:
```console
git submodule update --init
sudo apt install python3.8-venv
```

### Build the example applications

The examples can be built with [Arm Compiler for Embedded](https://developer.arm.com/Tools%20and%20Software/Arm%20Compiler%20for%20Embedded) or [Arm GNU Toolchain](https://developer.arm.com/Tools%20and%20Software/GNU%20Toolchain).\
This will take a few minutes to complete.

{{< tabpane code=true >}}
  {{< tab header="Arm Compiler for Embedded" >}}
./build_default.py --toolchain arm
{{< /tab >}}
  {{< tab header="GCC" >}}
./build_default.py
{{< /tab >}}
{{< /tabpane >}}

When complete, you will find the example images (`.axf` files) in the `cmake-build-*/bin` directory. Navigate to that directory.
```console
cd cmake-build-mps3-sse-300-ethos-u55-128-arm/bin
```
### Run an example
To run an example, launch the Virtual Hardware with one of the images, for example:
```console
VHT_Corstone_SSE-300_Ethos-U55 -a ethos-u-kws.axf
```
Note that the virtual hardware takes some time (approx 1 minute) to initialize the NPU. Be patient.

## Setting model parameters (Optional)

Some additonal parameters can be specified to Arm Virtual Hardware to configure certain aspects of how it executes.

### List parameters

For a full list of the available parameters, launch the executable with the `--list-params` option, for example:
```console
VHT_Corstone_SSE-300_Ethos-U55 --list-params > parameters.txt
```
### Set parameters
Parameters can be set with the `-C` option along with the parameter setting.\
For example, to put the Ethos-U component into fast execution mode:
```console
VHT_Corstone_SSE-300_Ethos-U55 -a ethos-u-kws.axf -C ethosu.extra_args="--fast"
```

If you wish to set many parameters, you may find it easier to list them in a text file (without `-C`) and use `-f` to specify that file.\
For example, create an `options.txt` containing:
```console
mps3_board.visualisation.disable-visualisation=1
ethosu.extra_args="--fast"
```
and specify with:
```console
VHT_Corstone_SSE-300_Ethos-U55 -a ethos-u-kws.axf -f options.txt
```

## Next Steps

The ML Evaluation Kit provides some stand alone ML examples. These building blocks have been integrated into complete software stacks in the [Open-IoT-SDK](/iot/total-solutions/total-iot).

[<-- Return to Learning Path](/iot/total-solutions/#sections)
