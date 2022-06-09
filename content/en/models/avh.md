---
title: "Getting Started with Arm Virtual Hardware"
linkTitle: "Get Started with Arm Virtual Hardware"
type: docs
weight: 1
description: >-
     This article describes how to get started with and set up Arm Virtual Hardware. 
---

## Introduction
 
[Arm Virtual Hardware (AVH)](https://developer.arm.com/Tools%20and%20Software/Arm%20Virtual%20Hardware) delivers ready-to-use models of Arm-based processors, systems and third party hardware. Arm Virtual Hardware runs as an application in the cloud to simplify, automate, accelerate and cost-reduce maintenance and development processes. 

## Pre-requisites
Arm provides a ready-to-use Amazon Machine Image (AMI) on AWS Marketplace. This is a Linux Virtual Machine that contains fully operational Virtual Hardware Targets, compilers and useful software utilities. It gives a lot of flexibility to integrate the Arm Virtual Hardware in various CI/CD DevOps environments. [AMI Inventory](https://arm-software.github.io/AVH/main/infrastructure/html/ami_inventory.html) gives the full list of resources available on the AVH AMI.

To use the Arm Virtual Hardware Service you first need an active AWS account. See corresponding AWS tutorial: [How do I create and activate a new AWS account?](https://aws.amazon.com/premiumsupport/knowledge-center/create-and-activate-aws-account/).

## Download installer packages {#download}

From your AWS account subscribe to Arm Virtual Hardware as follows:

Open [AWS Marketplace](https://aws.amazon.com/marketplace/search/results?searchTerms=Arm+Virtual+Hardware) and search for Arm Virtual Hardware.
Click on Arm Virtual Hardware to open the product page.
Click on Continue to Subscribe and then click Accept Terms to activate the subscription.
With the AVH Subscription you can now create and use AVH AMI instances. 

EC2 Instance type:

At least t2.micro instance type is required to run AVH AMI, while t3.medium is a recommended option. An instance with more resources may improve the performance.

## Setting up product license {#license}

The license is pre-installed on the AVH AMI for all the tools that are license managed. The .bash_rc file in the AVH AMI setups up the enviroment variable for the license file. 

`export ARMLMD_LICENSE_FILE=/opt/data.dat`

## Get started {#start}

To verify everything is working OK and to get started with the AVH AMI, follow the instructions [here](https://arm-software.github.io/AVH/main/infrastructure/html/run_ami_local.html). It walks you through the steps to:
* Launch AMI Instance .
* Connect to the AMI Instance .
* Run projects using launched AMI instance.
* Terminate the AMI instance once it is no longer required.
