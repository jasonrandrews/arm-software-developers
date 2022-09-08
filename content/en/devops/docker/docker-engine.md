---
title: "Install Docker Engine on Linux"
linkTitle: "Install Docker Engine on Linux"
type: docs
weight: 1
hide_summary: true
description: >-
     This article describes how to install Docker Engine on any Linux distribution
---

### Install and test Docker Engine

For any Linux machine, the commands below will install docker.

These commands are the (almost) universal install instructions for Docker on Linux.

The architecture can be x86_64 or Arm, including a cloud server and a Raspberry Pi.

The commands can also be used in the Windows Subsystem for Linux (WSL) and on a Chromebook.

For information about starting the docker daemon on WSL refer to [Install Docker on Windows on Arm](/devops/docker/docker-woa).

```console
curl -fsSL get.docker.com -o get-docker.sh && sh get-docker.sh
sudo usermod -aG docker $USER ; newgrp docker
```

To confirm the installation is successful run:

```console
docker run hello-world
```

The output should be a welcome message such as:

```console
Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (arm64v8)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/

```

To identify the architecture of the machine use the uname command:

```console
uname -m
```
Output values can be aarch64 (Arm 64-bit), armv7l (Arm 32-bit) or x86_64. 

### Docker Engine versions

The Stable channel (get.docker.com) provides the latest releases for general availability.

The Test channel (test.docker.com) installs pre-releases that are for testing before general availability (GA). 

Replace get.docker.com with test.docker.com to use the test version.

### Linux distributions where [get.docker.com](https://get.docker.com) isn't supported

Some Linux distributions are not supported by get.docker.com

Generally, the supported list is:
* Ubuntu
* Debian
* SUSE Linux Enterprise Server
* Red Hat Enterprise Linux
* Fedora
* CentOS

An example of a distribution which is not supported and popular on Arm is [Manjaro](https://manjaro.org).

On Manjaro, install docker using pacman.

```console
sudo pacman -Syu 
sudo pacman -S docker
sudo systemctl enable docker
sudo systemctl start docker
sudo usermod -aG docker $USER ; newgrp docker
```

To confirm the installation is successful run the same hello-world as above.

```console
docker run hello-world
```

### Start and Stop the Docker daemon on Linux distributions with systemd

To start the docker daemon.

```console
sudo systemctl start docker
```

To stop the docker daemon.

```console
sudo systemctl stop docker
```

If a message is displayed:
```console
Warning: Stopping docker.service, but it can still be activated by:
  docker.socket
```

Then stop docker.socket also.
```console
sudo systemctl stop docker.socket
```

### More information

Refer to the [Installation instructions](https://docs.docker.com/engine/install/) for more information about installing Docker Engine on Linux.



