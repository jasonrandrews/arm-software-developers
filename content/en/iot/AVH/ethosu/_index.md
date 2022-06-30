---
title: "Evaluate Ethos-U for ML applications"
linkTitle: "Evaluate Ethos-U for ML applications"
type: docs
weight: 30
description: >
    Learn about the Ethos-U Evaluation Kit and how to use it with Corstone-300 and Arm Virtual Hardware
---
Developers have access to an easy to use platform to develop powerful embedded and IoT applications, making use of the latest Machine Learning (ML) technology from Arm. [Arm Virtual Hardware](https://www.arm.com/en/products/development-tools/simulation/virtual-hardware) provides a growing number of platforms to get started with software development. In parallel, Arm has developed the [Ethos-U Evaluation Kit](https://review.mlplatform.org/plugins/gitiles/ml/ethos-u/ml-embedded-evaluation-kit), which includes ready-to-use ML applications. These allow you to investigate the embedded software stack and evaluate performance of the networks running on the Cortex-M55 and Ethos-U55 processors.

The Virtual Hardware is also a digital twin of the [MPS3](https://developer.arm.com/en/dev2/Tools%20and%20Software/MPS3%20FPGA%20Prototyping%20Board) FPGA image ([Application Note 547](https://developer.arm.com/downloads/-/download-fpga-images)). This enables easy code migration from a virtual to a physical platform, allowing for real-world trials of your application.

## Get Started

To get started, launch an Arm Virtual Hardware [session](https://avh.arm.com) on AWS. This invokes a cloud based instance of Ubuntu Linux with all necessary Arm toolc pre-installed. Alternatively you can use your own local environment. For tooling installation instructions, see [Getting Started](/successkits/install)

Clone the Evaluation kit repo

`git clone "https://review.mlplatform.org/ml/ethos-u/ml-embedded-evaluation-kit"`\
`cd ml-embedded-evaluation-kit`

Resolve external dependencies and prepare build environment

`git submodule update --init`\
`sudo apt install python3.8-venv`

Build the example applications with [Arm Compiler for Embedded](https://developer.arm.com/Tools%20and%20Software/Arm%20Compiler%20for%20Embedded). Note that this will take a few minutes to complete.

`./build_default.py --toolchain arm`

When complete, you will find the example images (`.axf` files) in the `cmake/bin` directory, likely:

`/ml-embedded-evaluation-kit/cmake-build-mps3-sse-300-ethos-u55-128-arm/bin`

To run an example, launch the Virtual hardware with one of the images, for example:

`VHT_Corstone_SSE-300_Ethos-U55 -a ethos-u-kws.axf`

Note that the virtual hardware takes some time (approx 1 minute) to initialize.

Full instructions are provided in the [documentation](https://review.mlplatform.org/plugins/gitiles/ml/ethos-u/ml-embedded-evaluation-kit/+/HEAD/docs/quick_start.md)

## Setting model parameters

Some additonal parameters can be specified to Arm Virtual Hardware to configure certain aspects of how it executes. For a full list of the available parameters, launch the executable with the `--list-params` option, for example:

`VHT_Corstone_SSE-300_Ethos-U55 --list-params > parameters.txt`

Parameters can be set with the `-C` option along with the parameter setting. For example, to put the Ethos-U component into fast execution mode:

`VHT_Corstone_SSE-300_Ethos-U55 -a ethos-u-kws.axf -C ethosu.extra_args="--fast"`

If you wish to set many parameters, you may find it easier to list them in a test file (without `-C`) and use `-f` to specify that file.

`VHT_Corstone_SSE-300_Ethos-U55 -a ethos-u-kws.axf -f options.txt`

## Next Steps

The Ethos-U Evaluation Kit provides some ready made ML examples. To see how these integrate into a complete software stack, see [Arm Total Solutions for IoT](https://www.arm.com/solutions/iot/total-solutions-iot)

 - [Get started with Arm Total Solutions for IoT](/iot/avh/total)
 