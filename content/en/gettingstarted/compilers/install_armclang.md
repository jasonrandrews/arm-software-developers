---
title: "Download and install Arm Compiler for Embedded"
linkTitle: "Installing the Arm Compiler"
type: docs
weight: 1
description: >-
     This article describes how to download and install appropriate versions of the Arm Compiler for Embedded, and Arm Compiler for Embedded FuSa
---

## Introduction

There are many versions of the [Arm Compiler for Embedded](https://developer.arm.com/Tools%20and%20Software/Arm%20Compiler%20for%20Embedded) toolchain available for use. In general, the latest version is recommended for use, as this will contain the latest optimization improvements, as well as support for the latest Arm IP. However there are reasons you may wish to use earlier compiler versions, especially where Functional Safety is concerned, where a specific compiler version is often mandated. A special branch of Arm Compiler for Embedded, known as [Arm Compiler for Embedded FuSa](https://developer.arm.com/downloads/-/arm-compiler-for-functional-safety), is available for this use case.

## Using the compiler supplied with Arm Development Studio {#armds}

The easiest way to access and setup the compiler is to use the version provided with [Arm Development Studio](https://developer.arm.com/Tools%20and%20Software/Arm%20Development%20Studio). The particular Development Studio version will contain the latest compiler version available at the time of release of that version, and is generally up to date with the stand alone compiler.

Note: Arm Compiler for Embedded FuSa is NOT installed as part of Arm Development Studio.\
Note: Cortex-M users can also use the compiler as provided with [Keil MDK](https://www2.keil.com/mdk5).

## Download standalone compiler packages {#download}

Individual compiler packages can be downloaded from the Product Downloads section of the Arm website.

[Arm Compiler for Embedded](https://developer.arm.com/downloads/-/arm-compiler-for-embedded)\
[Arm Compiler for Embedded FuSa](https://developer.arm.com/downloads/-/arm-compiler-for-functional-safety)

These can either be used standalone (note license setup below) or with your Arm Development Studio installation. For the latter, you must first [register](https://developer.arm.com/documentation/101469/latest/Installing-and-configuring-Arm-Development-Studio/Register-a-compiler-toolchain) your new compiler installation with Development Studio, before then [configuring](https://developer.arm.com/documentation/101469/latest/Installing-and-configuring-Arm-Development-Studio/Register-a-compiler-toolchain/Configure-a-compiler-toolchain-for-the-Arm-DS-command-prompt) the environment to use that version.

## Setting up product license {#license}

Arm Compiler for Embedded and Arm Compiler for Embedded FuSa are license managed. They can be enabled by a [Success Kit](https://www.arm.com/products/development-tools/success-kits), Arm Development Studio (Gold Edition for FuSa), or a standalone license. If you are unsure what you have access to, please contact your Arm representative. Subscribers to programs such as [Arm Flexible Access](https://www.arm.com/products/flexible-access) have success kit licenses available.

Since Arm Compiler for Embedded 6.18, and Arm Compiler for Embedded FuSa 6.16.2, Arm User-based licensing (UBL) is supported. To check if you have such a license enabled, use the `armlm inspect` command. If a license is reported, then you are ready to use Arm Compiler (and other Arm tools).

If no license is listed, you must [activate](https://developer.arm.com/documentation/102516/latest/Using-user-based-licensing) your license appropriately.\
If no license is listed, you must [activate(internal link)](https://developer.arm.com/documentation-preview/102516/latest/Using-user-based-licensing) your license appropriately.

If using earlier compiler versions standalone or if no UBL license is available, you will need to set the environment variable `ARM_PRODUCT_DEF` to the `\\sw\mappings\product.elmap` file of your compiler installation, and ensure the environment variable `ARMLMD_LICENSE_FILE` is set to an appropriate license server. See [this article](https://developer.arm.com/documentation/ka004977/latest) for more details.

## Get started {#start}

To check that the correct compiler version is being used, enter `armclang --version`.\
To verify everything is working OK, you can build a simple `Hello World` example by following the instructions [here](https://developer.arm.com/documentation/100748/latest/Getting-Started/Compiling-a-Hello-World-example).