---
title: "Get Started with Arm Fast Models"
linkTitle: "Get Started with Fast Models"
type: docs
weight: 1
description: >-
     This article describes how to set up Arm Fast Models for standalone use. If using Fast Models within an EDA partner's environment, please contact the relevant vendor for guidance.
---

## Introduction

[Arm Fast Models](https://developer.arm.com/Tools%20and%20Software/Fast%20Models) are accurate, flexible programmer's view models of Arm IP. They are used to build a virtual platform, either standalone, or as part of Hybrid Simulation environment within EDA partner environments. Use the virtual platform for software development and verification throughout the development process, even long before any real hardware is available.

This article discusses the stand alone use case. If using as part of an EDA partner's environment, please contact the relevant vendor for guidance.

## Pre-requisites

A Fast Model based virtual platform is an executable that runs on your Linux or Windows host. You must ensure that the appropriate host toolchain is installed.

For Linux hosts, use `gcc 9.3.0`\
For Windows hosts use [Visual Studio 2019](https://visualstudio.microsoft.com/vs/older-downloads/) 16.7.3 (or later). Express or Community editions can NOT be used.

More information is given in [the documentation](https://developer.arm.com/documentation/100965/1117/Installing-Fast-Models/Requirements-for-Fast-Models).

## Download installer packages {#download}

You can download the Fast Models installer and examples suite from the [Product Downloads section]((https://developer.arm.com/downloads/-/fast-models)) of the Arm website. Linux and Windows hosts are supported.

Full installation instructions are provided [here](https://developer.arm.com/documentation/100965/latest/Installing-Fast-Models/Installation).

Windows users, once installed, open the System Canvas IDE, and select File > Preferences > Applications, and locate the folder containing `devenv.com` in your Visual Studio installation (`\\Common7\IDE`).

## Setting up product license {#license}

All Arm Fast Models are license managed, and are enabled by a [Success Kit](https://www.arm.com/products/development-tools/success-kits). To build and edit your virtual platform, a Hardware Success Kit license is required. If you need to only execute an existing built model, then a Software (or Hardware) Success Kit license will be needed.

Since Arm Fast Models 11.17, Arm User-based licensing (UBL) is supported. To check if you have such a license enabled, use the `armlm inspect` command. If a license is reported, then you are ready to use Arm Fast Models (and other Arm tools).

If no license is listed, you must [activate](https://developer.arm.com/documentation/102516/latest/Using-user-based-licensing) your license appropriately.

If using earlier versions or if no UBL license is available, you will need to set the environment variable `ARMLMD_LICENSE_FILE` is set to an appropriate license file or server. You can set this as part of the GUI installation process.

## Get started {#start}

To verify everything is working OK, you can build one of the many example projects provided.

 - Launch the System Canvas IDE, and select `File` > `Load Project`, and browse to the `FastModelsPortfolio_<version>\examples' folder.
 - Select any example (such as `\LISA\FVP_MPS2\Build_Cortex-M3\FVP_MPS2_Cortex-M3.sgproj`).
 - Ensure an appropriate Project Configuration is selected from the pulldown in the upper toolbar (such as `Win64_Release-VC19`).
 - Click `Build` in the upper toolbar to build the virtual platform.
 - Once built, click `Run` and select `ISIM system` before launching the virtual platform.\
   - If a suitable program image is available (such as the `startup_Cortex-M3_AC6.axf` example from [Arm Development Studio](https://developer.arm.com/Tools%20and%20Software/Arm%20Development%20Studio)), you can load this with the `-a` option.

## Further Reading

   [Common tasks: Get started with Arm Fast Models](https://developer.arm.com/documentation/102441)
