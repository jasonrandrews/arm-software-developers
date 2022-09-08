---
processors: ["Neoverse-N1"]
software: ["linux","docker"]
title: "Remote Docker builds on an Arm server" 
linkTitle: "Remote Docker builds on an Arm server" 
type: docs
weight: 4
hide_summary: true
description: >
    Build a Docker image on a remote Arm server
---

## Pre-requisites

* Docker should be installed before starting. To install Docker follow refer to [Installing Docker](/devops/docker).
* Test docker using the hello-world image
```console
docker run hello-world
```
* Use the uname command to know your machine architecture
```console
uname -m 
```

Docker should also be installed on a remote machine of a different architecture which can be reached via ssh without password. 

For more information about ssh configuration refer to [TODO]().

## Detailed Steps

This a simple introduction to using the docker context command to build an image for another architecture using a remote machine accessible via ssh. 

### Build a simple Dockerfile to print the machine architecture

Create a new directory and save the two lines below into a file named Dockerfile, or re-use the same file from the previous How-To.
```dockerfile
FROM ubuntu:latest
CMD echo -n "Architecture is " && uname -m
```

Build the docker image using docker build. This creates an image for the local machine architecture.

```console 
docker build -t uname .
```

If the build is complex and requires long execution time using a remote builder may provide better performance than using buildx and architecture emulation. For example, building a large C++ project may have significant slowdown with buildx. 

```console
docker context create remote --docker "host=ssh://username@IP"
docker context use remote
```

As soon as the remote context is set, commands like **docker images** show the images on the remote machine, not the local images. 

To build an image on the remote machine use docker build.

```console
docker build -t jasonrandrews/uname  .
```

If you manually ssh to the remote machine and use **docker images** the list should be the same as on the local machine with the remote context set. 

Run the image, this runs on the remote machine.

```console
docker run --rm jasonrandrews/uname
```

The output is the architecture of the remote machine. 

Push the image to Docker Hub. It will go directly from the remote machine to Docker Hub. 

```console
docker push jasonrandrews/uname
```

To run the image on the local machine change the context back to default. 

```console
docker context use default
```

The **docker images** command shows the image is not on the local machine. 

Run the image on the local machine. It will pull from Docker Hub and run. 

If the architecture is different, use the platform flag to set the architecture matching the remote machine.

```console
docker run --rm --platform linux/amd64 jasonrandrews/uname
```

A remote docker daemon is a powerful concept, but it can be tricky to manage the context and remember which machine is being used. 

[<-- Return to Learning Path](/cloud/docker/#sections)
