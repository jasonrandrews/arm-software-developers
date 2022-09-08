---
processors: ["Neoverse-N1"]
software: ["linux","docker"]
title: "Docker build for single-architecture builds"
linkTitle: "Docker build for single-architecture builds"
type: docs
weight: 1
hide_summary: true
description: >
    This article is a simple demonstration of docker build on any machine.
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

## Detailed Steps

This a simple introduction to Docker for a single-architecture image using docker build.

### Build a simple Dockerfile to print the machine architecture

Create a new directory and save the two lines below into a file named Dockerfile 
```dockerfile
FROM ubuntu:latest
CMD echo -n "Architecture is " && uname -m
```

Build the docker image using docker build.

```console 
docker build -t uname .
```

### Run the simple image 

Run the image to print the architecture. 

```console
docker run --rm uname 
```

Use the Docker images command to see the image:
```console
docker images
```
The output will be similar to:
```console
REPOSITORY   TAG       IMAGE ID       CREATED      SIZE
uname        latest    f0a8125a81d3   5 days ago   69.2MB
```

The Docker image can be run on any computer with the same architecture it was created on. 

If the machine uses the Intel architecture the output will be:
```console
Architecture is x64_86
```

If the machine uses the Arm architecture the output will be:
```console
Architecture is aarch64
```

Other architecture values are possible. 

Arm 32-bit Linux will print:
```console
Architecture is armv7l
```

On macOS with Apple Silicon the output will be:
```console
Architecture is arm64
```

Docker image names have the form **repository/image-name:tag** 

In the example above the image name is uname and the tag name (default) is latest. 

To tag the image for Docker Hub put a username for a Docker Hub account in front of the image name, in the repository field. 

Change jasonrandrews to your Docker Hub username. 

The tag of "latest" can be ommitted since it is the default value. 

```console
docker tag uname:latest jasonrandrews/uname:latest
```

To save the image on Docker Hub use the push command.
```console
docker push jasonrandrews/uname:latest
```

With the default tag of "latest" it is difficult to tell which architecture the image is for. Looking at the image on Docker Hub will show the architecture, but it's not very clear.

Running a Docker image on a computer with a different architecture from the one it was created on doesn't automatically work because the computers have different instructions sets.

One way to solve the problem is to make a different image on every architecture and then tell the user of the image to get the correct one. 

This is not ideal because it means a user must change the details of retrieving the image depending on the computer. This results in scripts with "if statements" based on architecture.

Another way is to create multi-architecture images. 

With multi-architecture images the user can run the image on any architecture and Docker will autoamtically get the correct image.

Continue the learning path to learn about multi-architecture images. 

[<-- Return to Learning Path](/cloud/docker/#sections)
