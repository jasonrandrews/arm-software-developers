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

Note that it is possible to use SSH instead to connect to the instance(s). See the `Connect` tab for instructions.\
Depending on your network, you may need to use [OpenVPN Community](https://openvpn.net/community-downloads/) to connect remotely via SSH.

It is also possible to log in via the simulated LCD screen, however it is not recommended for this workshop, as it is not possible to copy and paste to this interface.

For this workshop, we shall use Console interface in the browser.

### Install necessary software components

We shall build the Matter examples on the virtual Raspberry Pi 4 instances. To prepare for this install the necessary dependencies on **each** instance.
```console
sudo apt-get update
sudo apt-get install git gcc g++ python pkg-config libssl-dev libdbus-1-dev libglib2.0-dev libavahi-client-dev ninja-build python3-venv python3-dev python3-pip unzip libgirepository1.0-dev libcairo2-dev libreadline-dev
```
This will also help verify that your instances are working correctly.

### Snapshots (optional)

We have now successfully launched two Arm Virtual Hardware instances of Raspberry Pi 4. It is possible to create a `Snapshot` of an instance, such that you can automatically restore to that point if necessary (for example if you wish to undo changes you make later). This is particularly useful when using Arm Virtual Hardware in CI/CD flow.

To create a Snapshot, you must power down the instance with the `Power` button. Click the `Snapshots` tab, and `Take New Snapshot`. If you ever wish to return your instance to this point in time, click `Restore` for that Snapshot.

## Next Steps

[<-- Return to Workshop](/devsummit22/#sections)
