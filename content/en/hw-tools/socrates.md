---
title: "Getting Started with Arm Socrates"
linkTitle: "Get Started with Socrates"
type: docs
weight: 1
description: >-
     This article describes how to set up and get started with Arm Socrates.
---

## Introduction

[Arm Socrates](https://developer.arm.com/Tools%20and%20Software/Socrates) is a tool used to select, configure and create Arm IP for easy and error free integration into a System on Chip(SoC). 

This article discusses how to download, install and get started with Socrates.

## Pre-requisites

Arm Socrates tooling requires a Linux host machine. Full specifications are given in section 3.2 of the [Installation Guide](https://developer.arm.com/documentation/101400)

## Download installer packages {#download}

Socrates is available through Arm Flexible Access(AFA), which gives access to IP, relevant tools and models, and support. The tool is pacakged within [Arm Success Kits](https://www.arm.com/products/development-tools/success-kits). 
All AFA downloads are provided via the [Arm Product Download Hub](https://developer.arm.com/downloads). You will need to set up an account for this system to be able to download. It may be that only certain contacts within your organization have such access. If you are unsure, please contact your Arm account manager for assistance.

You can download Socrates as an individual standalone component, or you can download the complete success kits. The installer is available for Linux only.

Full installation instructions are provided [here](https://developer.arm.com/documentation/101400).

## Setting up product license {#license}

Arm Socrates Tool is license managed, and is enabled by a [Hardware Success Kit](https://www.arm.com/products/development-tools/success-kits) license. Configuration of some Arm IP products require a corresponding license for that IP.

You will need to set the environment variable `ARMLMD_LICENSE_FILE` to an appropriate license server. Full details for this are provided in Section 5 "Setting up the License" of the [Installation Guide](https://developer.arm.com/documentation/101400).

## Get started {#start}

To check Socrates has installed correctly, use the socrates.sh command or double‑click the Socrates™ icon to start Socrates™.
You can run socrates.sh directly from the installation location, through an alias to the installation location, or you can add the installation location to your path variable.

There is an Installation Health Check script provided that runs the first time that you start the software, or the first time that you run a new version. The script checks that all required dependencies are installed and identifies any common installation problems.

Arm has produced a series of videos to help new users get started and learn how to use the tool.\
They are available on the [Arm YouTube channel](https://www.youtube.com/c/arm):

 * [Getting Started](https://youtube.com/playlist?list=PLgyFKd2HIZlY_y7b5OTtyrso45q-eCM_s)
 * [NIC-400 Configuration](https://youtube.com/playlist?list=PLgyFKd2HIZlaQBfd8YEMwSQX_cWIxODgG)
 * [NI-700 Configuration](https://youtube.com/playlist?list=PLgyFKd2HIZlahIsHSSw7ViwiFxeBYc36b)