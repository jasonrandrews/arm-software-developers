---
title: "Debugging Arm Fast Models with Arm Development Studio"
linkTitle: "Debug Fast Models with Arm DS"
type: docs
weight: 100
description: >-
     This article describes how to set up an Arm Development Studio debug connection with your Arm Fast Model virtual platform.
---

## Introduction

[Arm Fast Models](https://developer.arm.com/Tools%20and%20Software/Fast%20Models) are accurate, flexible programmer's view models of Arm IP. They are used to build a virtual platform, either standalone, or as part of Hybrid Simulation environment within EDA partner environments. Use the virtual platform for software development and verification throughout the development process, even long before any real hardware is available.

You can connect the [Arm Development Studio](https://developer.arm.com/Tools%20and%20Software/Arm%20Development%20Studio) debugger to your virtual platform and interact with it as if were real hardware.

## Pre-requisites

It is assumed that you have Arm Development Studio and Fast Models installed and setup.
- [Get Started with Fast Models]({{< relref "models/start_fm.md" >}})
- [Get Started with Arm Development Studio]({{< relref "getstarted/armds.md" >}})

In this example we shall use the supplied `FVP_MPS2_Cortex-M3` Fast Models example, along with the `startup_Cortex-M3_AC6` software example as supplied with Arm Development Studio.

In `System Canvas`, load the `FVP_MPS2_Cortex-M3` project and build.\
In `Arm Development Studio IDE` import the example via `File` > `Import...` > `Arm Development Studio` > `Examples and Programming Libraries`, and browsing for `startup_Cortex-M3_AC6`.

## Create a Model Configuration for your Virtual Platform {#modelconfig}

In the debugger menu, select `File` > `New` > `Other` > `Configuration Database` > `Configuration Database`, and give it a meaningful name. This is where the debugger stores all user-made configurations.

Then select `File` > `New` > `Other` > `Configuration Database` > `Model Configuration`, which will be the actual configuration we wish to create. When prompted, select the above `Configuration Database`.

You may then be prompted to ask which debug interface to use, `Iris` or `CADI`. `Iris` is the default and recommended interface.

You are then prompted to either launch the model, or browse for an already running model:

### Launch and connect to specific model

If this is selected, simply browse for the Fast Model executable on your host. The debugger will append necessary command options to enable debug.

### Browse for model running on local host

If this is selected, you must launch the Fast Model either from the command line, else via `System Canvas` > `Run` dialog, with `-I` option to start the Iris server in the model. If no port number (`--port-number`) is specified, recommend adding `-p` to output the port number used.

### Browse for model running on remote host

If this is selected (where the virtual platform is running on a different machine on the network), you must launch the Fast Model either from the command line, else via `System Canvas` > `Run` dialog, with `-I -A` options to start the Iris server in the model and allow remote access. If no port number (`--port-number`) is specified, recommend adding `-p` to output the port number used. You will be prompted for the server address (the machine running the virtual platform) and port number.

Regardless of how you connect to the model, a `.mdf` file will be created. Specify a manufacturer and platform name, and click Import.

## Create a Debug Configuration for your Virtual Platform {#debugconfig}

Now that the debugger is aware of your virtual platform, you can now create a debug configuration to describe how the debugger will connect to that platform.

To start, select `File` > `New` > `Model Connection`, and give it a meaningful name. It is recommended to associate the connection with a specific project (`startup_Cortex-M3_AC6`) when available.

Select the model connection you created (the text filter can assist if many targets defined), and click Finish.

Note that you can bypass the above steps if you prefer by clicking `Debug` within the model configuration view.

You can again select to launch a new instance of the model or connect to an already running model.

### Launch a new model

No further configuration needed.

### Browse for model running on local host

If this is selected, you must launch the Fast Model either from the command line, else via `System Canvas` > `Run` dialog, with `-I` option to start the Iris server in the model. If no port number (`--port-number`) is specified, recommend adding `-p` to output the port number used.

Specify the connection address as `localhost:<port>`

### Browse for model running on remote host

If this is selected (where the virtual platform is running on a different machine on the network), you must launch the Fast Model either from the command line, else via `System Canvas` > `Run` dialog, with `-I -A` options to start the Iris server in the model and allow remote access. If no port number (`--port-number`) is specified, recommend adding `-p` to output the port number used. You will be prompted for the server address (the machine running the virtual platform) and port number.

Specify the connection address as `hostname:<port>`

To load an image, navigate to the `Files` tab, and browse to the `startup_Cortex-M3_AC6.axf` pre-built image. Then, in the `Debugger` tab, select `Debug from entry point`.\
If the model is already running with an image (`-a <image>`), you can also just the debug symbols from the `Files` tab. In that scenario, in the `Debugger` tab, select `Connect Only`.\
Click OK to connect to the virtual platform, and commence your debug session.