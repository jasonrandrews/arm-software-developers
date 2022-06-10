---
title: "Getting Started with Arm Socrates"
linkTitle: "Get Started with Socrates"
type: docs
weight: 1
description: >-
     This article describes how to set up and get started with Arm Socrates.
---

## Introduction

[Arm Socrates](https://developer.arm.com/Tools%20and%20Software/Socrates) is a tool used to configure and create Arm IP for easy and error free integration into a System on Chip(SoC). 

This article discusses how to download, install and get started with Socrates.

## Pre-requisites

A Fast Model based virtual platform is an executable that runs on your Linux or Windows host. You must ensure that the appropriate host toolchain is installed.

For Linux hosts, use gcc 9.3.0\
For Windows hosts use [Visual Studio 2019](https://visualstudio.microsoft.com/vs/older-downloads/) 16.7.3 (or later). Express or Community editions can NOT be used.

More information is given in [the documentation](https://developer.arm.com/documentation/100965/1117/Installing-Fast-Models/Requirements-for-Fast-Models).

## Download installer packages {#download}

Socrates is available through Arm Flexible Access(AFA), which gives access to IP, relevant tools and models, and support. The tool is pacakged within [Arm Success Kits](https://www.arm.com/products/development-tools/success-kits). 
All AFA downloads are provided via the [Arm Product Download Hub](https://developer.arm.com/downloads). You will need to set up an account for this system to be able to download. It may be that only certain contacts within your organization have such access. If you are unsure, please contact your Arm account manager for assistance.

You can download Socrates as an individual standalone component, or you can download the complete success kits. The installer is available for Linux only.

Full installation instructions are provided [here](https://developer.arm.com/documentation/101400/1-7-0/?lang=en).

## Setting up product license {#license}

Arm Socrates Tool is license managed, and is enabled by a [Success Kit](https://www.arm.com/products/development-tools/success-kits). A Hardware Success Kit license is required. 

Since Arm Socrates 11.17, Arm User-based licensing (UBL) is supported. To check if you have such a license enabled, use the `armlm inspect` command. If a license is reported, then you are ready to use Arm Fast Models (and other Arm tools).

If no license is listed, you must [activate](https://developer.arm.com/documentation/102516/latest/Using-user-based-licensing) your license appropriately.\
If no license is listed, you must [activate(internal link)](https://developer.arm.com/documentation-preview/102516/latest/Using-user-based-licensing) your license appropriately.

If using earlier versions or if no UBL license is available, you will need to set the environment variable `ARMLMD_LICENSE_FILE` is set to an appropriate license server. Full details for this are provided in Section 5 "Setting up the License" of the [Installation Guide](https://developer.arm.com/documentation/101400/1-7-0/?lang=en).

## Get started {#start}

To check Socrates has installed correctly, use the socrates.sh command or double‑click the Socrates™ icon to start Socrates™.
You can run socrates.sh directly from the installation location, through an alias to the installation location, or you can add the installation location to your path variable.
There is an Installation Health Check script provided that runs the first time that you start the software, or the first time that you run a new version. The script checks that all required dependencies are installed and identifies any common installation problems.

