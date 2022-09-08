
---
title: "Installing Docker"
linkTitle: "Installing Docker"
type: docs
weight: 1
hide_summary: true
description: >
    Learn how to install Docker on any computer and test it works
---

{{% pageinfo %}}
Docker containers are widely used, primarily because they run the same everywhere. Containers are used on all major operating systems, on all major computing architectures to build, share, and run software. 

The operating system of the computer and the architecture (x86_64 or Arm) will determine how to install Docker.

Select from the cards below to find out how to install and run Docker. 
{{% /pageinfo %}}

{{< cardpane >}}
{{< card header="**Docker Engine for Linux**" >}}

[Docker Engine for Linux](https://www.docker.com/products/container-runtime) is the most commonly used container runtime. It works on a variety of Linux distributions and architectures, including arm and arm64 (aarch64). Use these instructions for Linux and Linux running on Chrome OS

[Install Docker Engine on Linux](docker-engine)

{{< /card >}}

{{< card header="**Docker Desktop**" >}}

[Docker Desktop](https://www.docker.com/products/docker-desktop/) is he easiest way to install Docker on Windows and macOS.

The macOS version supports both Intel and Apple Silicon. The Windows version does not support Windows on Arm. 

There is also a new Docker Desktop for Linux avilable if the machine has KVM support and is running a KDE or Gnome desktop environment.

[Install Docker Desktop](docker-desktop)

{{< /card >}}

{{< card header="**Windows on Arm**">}}

Docker can be run on Windows on Arm machines using the Windows Subsystem for Linux 2 (WSL2). 

There is no Docker Desktop for Windows on Arm, [please show your support by asking for it](https://github.com/docker/roadmap/issues/91)

[Install Docker on Windows on Arm ](docker-woa)

{{< /card >}}

{{< /cardpane >}}


