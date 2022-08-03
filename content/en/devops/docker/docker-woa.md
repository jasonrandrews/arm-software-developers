---
title: "Install Docker on Windows on Arm"
linkTitle: "Install Docker on Windows on Arm"
type: docs
weight: 3
hide_summary: true
description: >-
     This article describes how to install Docker on a Windows on Arm computer
---

### Prerequisites

- Install WSL 2 on the Windows on Arm laptop
- Install a Linux distribution such as Ubuntu 22.04 Linux distribution in WSL 2 from the Microsoft Store

### Example Windows on Arm computers

- [Lenovo Thinkpad X13s](https://www.lenovo.com/us/en/p/laptops/thinkpad/thinkpadx/thinkpad-x13s-(13-inch-snapdragon)/len101t0019)
- [Microsoft Surface Pro X](https://www.microsoft.com/en-us/d/surface-pro-x/8xtmb6c575md?activetab=pivot%3aoverviewtab)
- [Samsung Galaxy Book S](https://www.samsung.com/us/computing/galaxy-books/galaxy-book-s/galaxy-book-s-256gb-mercury-gray-verizon-sm-w767vzaavzw/)

### Install and test Docker Engine

From within WSL2 running a Linux distribution on a Windows on Arm laptop, the general Linux install instructions can be used. 

```console
curl -fsSL test.docker.com -o get-docker.sh && sh get-docker.sh
sudo usermod -aG docker $USER ; newgrp docker
```

The Docker daemon will not automatically start in WSL 2. 

It can be started manually:
```console
sudo /etc/init.d/docker start
```

It can also be started automatically using by editing /etc/wsl2.conf

Add the info below to the file:

```console
# Set a command to run when a new WSL instance launches. This example starts the Docker container service.
[boot]
command = service docker start
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

### Docker Engine versions

The Stable channel (get.docker.com) provides the latest releases for general availability.

The Test channel (test.docker.com) installs pre-releases that are for testing before general availability (GA). 

Replace get.docker.com with test.docker.com to use the test version.


### More information

Refer to the [Installation instructions](https://docs.docker.com/engine/install/) for more information about installing Docker Engine on Linux.

There are numerous Linux distribution options from the Microsoft Store.

There is no Docker Desktop for Windows on Arm, [please show your support by asking for it](https://github.com/docker/roadmap/issues/91)

For more information about [installing WSL 2](https://docs.microsoft.com/en-us/windows/wsl/install)

