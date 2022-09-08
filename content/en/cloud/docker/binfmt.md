---
processors: ["Neoverse-N1"]
software: ["linux","docker"]
title: "Install binfmt for multi-architecutre support on Linux"
linkTitle: "Install binfmt for multi-architecutre support on Linux"
type: docs
weight: 3
hide_summary: true
description: >
    Install multi-architecture support on Linux
---

## Pre-requisites

* Docker should be installed before starting. To install Docker follow refer to [Installing Docker](/devops/docker).
* Test docker using the hello-world image
```console
docker run hello-world
```
* Docker buildx should also be installed. It is available in recent versions of docker. 
```console
docker buildx help
```
* Use the uname command to know your machine architecture
```console
uname -m 
```

This information is only for machines WITHOUT Docker Desktop.


## Detailed Steps

The multi-architecture features demonstrated in [Docker buildx for multi-architecture builds](../buildx) work with Docker Desktop. For Linux machines without Docker Desktop extra software is required to build and run images for different architectures.

### Build a simple Dockerfile to print the machine architecture

Create a new directory and save the two lines below into a file named Dockerfile, or re-use the same file from the previous How-To.
```dockerfile
FROM ubuntu:latest
CMD echo -n "Architecture is " && uname -m
```

Build the docker image using docker build.

```console 
docker buildx create --use --name mybuilder
docker buildx build --platform linux/amd64,linux/arm64,linux/arm/v7 -t jasonrandrews/uname-x --push .
```

Try to run an architecture different from the current machine. 

On an x86_64 machine, try to run the aarch64 image.

```console
docker run --rm  --platform linux/arm64 jasonrandrews/uname-x
```

In some cases, the image may fail to run. 

The error message is similar to:
```console
standard_init_linux.go:228: exec user process caused: exec format error
```

To fix the error, architecture emulation support must be installed on the machine for other architectures. 

For Ubuntu install emulation support.

```console
sudo apt-get install qemu-user-static
```

Try again, and the multi-arch image will run successfully with the expected output.

```console
Architecture is aarch64
```

The installation should also install the binfmt-support Linux package. 

Instruction emulation using qemu and the ability to run applications for different architectures is built into Docker Desktop.

On Linux machies without Docker Desktop, qemu and binfmt can be added to provide the same multi-architecture support. 

[<-- Return to Learning Path](/cloud/docker/#sections)
