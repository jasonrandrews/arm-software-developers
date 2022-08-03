---
title: "Install Docker Desktop"
linkTitle: "Install Docker Desktop"
type: docs
weight: 2
hide_summary: true
description: >-
     This article describes how to install Docker Desktop on Windows or macOS
---

### Install and test Docker Desktop

All of the download files are available on the 
[Docker Desktop product page](https://www.docker.com/products/docker-desktop/).

Use the links below for more information

[Install Docker Desktop on Mac](https://docs.docker.com/desktop/install/mac-install) 

[Install Docker Desktop on Apple Silicon](https://docs.docker.com/desktop/mac/apple-silicon/) 

[Docker Desktop for Windows](https://docs.docker.com/desktop/install/windows-install/) 

[Docker Desktop for Linux](https://docs.docker.com/desktop/install/linux-install/) 

All of the Docker Desktop products use the x86_64 / amd64 architecture except macOS on Apple Silicon.

On any platform, To confirm the Docker Desktop installation is successful run:

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

To identify the architecture for macOS use the uname command. 

```console
uname -m
```
Apple Silicon will be reported as arm64


