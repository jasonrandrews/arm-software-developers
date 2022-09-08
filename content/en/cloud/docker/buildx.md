---
processors: ["Neoverse-N1"]
software: ["linux","docker"]
title: "Docker buildx for multi-architecture builds"
linkTitle: "Docker buildx for multi-architecture builds"
type: docs
weight: 2
hide_summary: true
description: >
    This article is a simple demonstration of docker buildx.
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

## Detailed Steps

This a simple introduction to Docker for a multi-architecture image using docker buildx.

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

Docker buildx must push the multi-architecture image to a registry. The docker daemon cannot save the image locally. This will change with the future transition from dockerd to containerd. 

The **docker images** command does not show a local image. The multi-arch image is present in Docker Hub. The missing local image is a common misunderstanding for developers.

### Run the image 

From any computer pull and run the multi-architecture image. Because support for 3 architectures is included, docker will automatically get the correct image and run it.

A pull is required because the image is not present on the local machine.

```console
docker run --rm jasonrandrews/uname-x
```

It's also possible to run the image for a different architecture than the current machine by adding --platform.

Depending on the architecture of the machine, pick a different platform and run the image using one of the commands.

```console
docker run --rm  --platform linux/arm64 jasonrandrews/uname-x
docker run --rm  --platform linux/arm/v7 jasonrandrews/uname-x
docker run --rm  --platform linux/amd64 jasonrandrews/uname-x
```

For example, on a machine with a uname of aarch64, run the amd64 image.

```console
docker run --rm  --platform linux/amd64 jasonrandrews/uname-x
```

The output will be:
```console
Architecture is x86_64
```

### Warning

It is possible to run buildx build again with a change to the Dockerfile, push to Docker Hub, and re-run expecting to run the new image.

The docker run command will use the local image. It will not pull the new version which went directly to Docker Hub. 

To remove the local copy use the **docker rmi** command.

```console
docker rmi jasonrandrews/uname-x
```

### Other useful commands

To list the builders

```console
docker buildx ls
```

To change to a different builder, such as default

```console
docker buildx use default
```

To remove a builder

```console
docker buildx rm mybuilder
```

[<-- Return to Learning Path](/cloud/docker/#sections)
