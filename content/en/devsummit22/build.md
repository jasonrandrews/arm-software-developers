---
title: "Build and run Matter examples on Arm Virtual Hardware"
linkTitle: "Build and run examples"
type: docs
toc_hide: true
hide_summary: true
description: >
    Build and run Matter examples on Arm Virtual Hardware.
---
## Overview

Learn how to build and run Matter examples on Arm Virtual Hardware.

## Pre-requisites

* Two Arm Virtual Hardware instances running in the cloud as per [previous section](/devsummit22/setup)
* GitHub account

## Detailed Instructions

### Fork Matter repository to your personal GitHub account

So that we can manage the development with GitHub actions later, we must create a personal fork of the public repository.

Browse to the Matter repo on Github
```console
https://github.com/project-chip/connectedhomeip
```

Click `Fork` in upper-right of screen, and create a fork in your own repository area.

### Clone your forked repository on your Virtual Hardware instances

Return to the `Console` tab of each of your Virtual Hardware instances, and clone your fork of the repository.
```console
git clone https://github.com/YOUR_GITHUB_USER_NAME/connectedhomeip.git
cd connectedhomeip
```
A number of submodules must also be cloned, which can be done with a provided script:
```console
./scripts/checkout_submodules.py --shallow --platform linux
```
Repeat on other Virtual Hardware instance.

### Prepare Matter Development Environment

Configure the Matter development environment on each instance, which again can be done with the provided script(s):
```console
./scripts/build/gn_bootstrap.sh
source scripts/activate.sh
```
These will take approximately 5 minutes to complete. Don't forget to run scripts on each instance, which you can perform in parallel. You should see
```
Environment looks good, you are ready to go!
```
when complete. Full [documentation](https://github.com/project-chip/connectedhomeip/blob/master/docs/guides/BUILDING.md) on the build environment is provided in the Matter repository.

### Build the examples

We are now ready to build the examples.

On one Virtual Hardware instance we shall build `chip-tool`, a Matter controller implementation that allows to commission a Matter device into the network and to communicate with it using Matter messages.
```console
cd examples/chip-tool
gn gen out/debug
ninja -C out/debug
```
In the other instance we shall build the reference `chip-lighting-app` for Linux, which will be controlled by the above `chip-tool`.
```console
cd examples/lighting-app/linux
gn gen out/debug
ninja -C out/debug
```
These builds can be performed in parallel. Confirm that both builds complete.

### Launch the chip-lighting-app

In the instance where `chip-lighting-app` was built, run that application.
```console
./out/debug/chip-lighting-app
```
The application will initialize, and you will see boot log echoed in the console. After approximately 20 seconds you will see in the log:
```
[TIMESTAMP][INSTANCEID] CHIP:DL: PlatformBlueZInit init success
```
Confirming it is ready to use (other messages in the log can be ignored). Full [documentation](https://github.com/project-chip/connectedhomeip/tree/master/examples/lighting-app/linux) for `chip-lighting-app` is provided in the repository.

Leave `chip-lighting-app` application running on this instance.

### Launch chip-tool

On the other instance, launch `chip-tool` and pair with the other instance, using:
```console
./out/debug/chip-tool pairing onnetwork-long 0x11 20202021 3840
```
You will see a long stream of messages echoed in console of both instances. Wait for this command to complete.

Full [documentation](https://github.com/project-chip/connectedhomeip/tree/master/examples/chip-tool) for `chip-tool` is provided in the repository.

### Control chip-lighting-app with chip-tool

The `chip-lighting-app` can now be controlled with `chip-tool`, simulating remote control of the application.

In the chip-tool instance, to send a message to turn the light ON, enter the command:
```console
./out/debug/chip-tool onoff on 0x11 1
```
Observe in the log of `chip-lighting-app` that this state is reflected with:
```
[TIMESTAMP][INSTANCEID] CHIP:ZCL: On/Off set value: 1 1
[TIMESTAMP][INSTANCEID] CHIP:ZCL: Toggle on/off from 0 to 1
```
Similarly to turn the light OFF, enter:
```console
./out/debug/chip-tool onoff off 0x11 1
```
And observe the `chip-lighting-app` log:
```
[TIMESTAMP][INSTANCEID] CHIP:ZCL: On/Off set value: 1 0
[TIMESTAMP][INSTANCEID] CHIP:ZCL: Toggle on/off from 1 to 0
```
## Next Steps

Congratulations! You have successfully enabled two Virtual Hardware instances to communicate to each other via Matter messages.

[<-- Return to Workshop Home](/devsummit22/#sections)
