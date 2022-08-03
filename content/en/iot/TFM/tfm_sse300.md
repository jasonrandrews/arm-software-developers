---
processors: [Cortex-M55]
software: [bare-metal]
title: "Run Trusted Firmware-M(TF-M) on Corstone-300 AVH FVP"
linkTitle: ""
type: docs
weight: 1
hide_summary: true
description: >
   Follow the instructions in this guide to build and run TF-M tests on Corstone-300 FVP included in AVH.
---

## Learning Objectives 

By the end of this guide, you will be able to:

* Build TF-M tests for the Corstone-300 AVH FVP 
* Run TF-M tests on the Corstone-300 AVH FVP

## Pre-requisites

* AWS Account
* AWS EC2 instance running AVH AMI. Use the instructions [here](iot/avh/launch)

## Detailed Steps

### Build the TF-M tests

On the launched EC2 instance running the AVH AMI, install python 3 pre-requisites for TF-M

```console
sudo apt update
sudo apt install python3.8-venv
sudo ln -s /usr/local/bin/pip3 /usr/bin/pip3.8
python3.8 -m pip install imgtool cbor2
python3.9 -m pip install imgtool cffi intelhex cbor2 cbor pytest click
```

Next, clone the TF-M git repository

```console
git clone https://git.trustedfirmware.org/TF-M/trusted-firmware-m.git
cd trusted-fimrware-m
```

TF-M uses cmake as the build system. Create a build directory, and then set the relevant cmake variables to build the TF-M suite of tests.

```console
mkdir cmake_build
cd cmake_build
cmake .. -DTFM_PLATFORM=arm/mps3/an552 -DTEST_NS=ON -DTEST_S=ON
```

In the command above we built both the secure and non-secure suite of TF-M tests. To build individual tests from these suites you can set the appropriate cmake variable instead. All the variables and options are defined in section 2.12 [here](https://tf-m-user-guide.trustedfirmware.org/docs/getting_started/tfm_build_instruction.html).

Finally, build using make

```console
make install
```

On a successful build, the TF-M test binaries are created in the bin/ directory. This includes binaries files for the MCUBoot bootloader, TF-M secure firmware and TF-M non-secure app. Signed variants of both the TF-M secure and non-secure images are created along with a combined signed image of both the secure and non-secure image.

### Run the TF-M tests on the Corstone-300 FVP

Now that we have successfully built the TF-M suite of tests, we are ready it to run it on the Corstone-300 FVP that is already installed on the AMI.

Use the command below to launch the simulation with the TF-M tests

```console
VHT_Corstone_SSE-300_Ethos-U55 -a cpu0*="bin/bl2.axf" --data "bin/tfm_s_ns_signed.bin"@0x01000000
```

bl2.axf is the MCUBoot bootloader image. tfm_s_ns_signed.bin is the combined signed image for the TF-M secure and non-secure image and the address after the @ sign indicates where in the Corstone-300 FVP memory the image is loaded. 

The memory map for the FVP is documented here https://developer.arm.com/documentation/100966/1118/Arm--Corstone-SSE-300-FVP/Memory-map-overview-for-Corstone-SSE-300


