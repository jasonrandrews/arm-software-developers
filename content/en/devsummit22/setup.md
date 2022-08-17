---
title: "Setup Arm Virtual Hardware (Raspberry Pi 4)"
linkTitle: "Setup Arm Virtual Hardware"
type: docs
toc_hide: true
hide_summary: true
description: >
    Setup Arm Virtual Hardware instances of Raspberry Pi 4.
---
## Overview

Learn how to setup and launch Arm Virtual Hardware instances.

## Pre-requisites

* User account for [Arm Virtual Hardware](https://avh.arm.com/)

## Detailed Instructions

### Login to Arm Virtual Hardware console

Open your browser, and navigate to Arm Virtual Hardware console:
```console
https://app.avh.arm.com/
```
### Create TWO Raspberry Pi 4 virtual devices

Click on `Create Device`.

Select `Raspberry Pi 4` from the list of available devices.

Select `Raspberry Pi OS lite` from the example firmware packages.

Give the device a meaningful name (suggest `chip-tool`), and create device.

While this is being created, click `Devices` and repeat steps to create a second instance (suggest `lighting-app` as name).

Open each instance in its own browser pane. We shall use these browser panes throughout the workshop.

### Login to virtual Raspberry Pi instances

When your instances are created, select the `Console` tab, and log into the instance.

Username: `pi`\
Password: `raspberry`

Repeat for the other instance.

### (Optional) Connect via SSH

To easily connect via SSH, you must download and install an appropriate [OpenVPN Community](https://openvpn.net/community-downloads/) version for your host.

In the Arm Virtual Hardware `CONNECT` tab, click on `DOWNLOAD OVPN FILE`.\
In OpenVPN, select `Import` > `Import file...` and browse to the downloaded `OVPN FILE`. Click `Connect`.\
On your host, open terminal(s), and connect to the virtual hardware instance(s) with the command shown in the `CONNECT` tab, or use your preferred terminal application.

It is possible to connect via SSH without the use of VPN.\
This requires some initial setup before launching the Virtual Hardware instance as described [here](/devsummit22/ssh).

The `CONSOLE` view within the browser will suffice for this workshop.

### Install necessary software components

We shall build the Matter examples on the virtual Raspberry Pi 4 instances. To prepare for this, install the necessary dependencies on **each** instance. This can be done im parallel.
```console
sudo apt-get update
sudo apt-get install git gcc g++ python pkg-config libssl-dev libdbus-1-dev libglib2.0-dev libavahi-client-dev ninja-build python3-venv python3-dev python3-pip unzip libgirepository1.0-dev libcairo2-dev libreadline-dev
```
This will also help verify that your instances are working correctly.

## Next Steps

If you wish to explore how closely the Virtual Hardware models real hardware, please see [this article](https://dev.to/aws-builders/welcome-to-the-virtual-raspberry-pi-4-running-on-aws-graviton-processors-2o8e).

[Proceed to next section -->](/devsummit22/build)\
[<-- Return to Workshop Home](/devsummit22/#sections)
