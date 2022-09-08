---
processors: ["Neoverse-N1"]
software: ["linux","docker"]
title: "Docker manifest for multi-architecture builds"
linkTitle: "Docker manifest for multi-architecture builds"
type: docs
weight: 5
hide_summary: true
description: >
    This article explains how create multi-architecture images using Docker manifest.
---

## Pre-requisites

* Docker should be installed before starting. To install Docker follow refer to [Installing Docker]](/devops/docker).
* Test docker using the hello-world image
```console
docker run hello-world
```
* Use the uname command to know your machine architecture
```console
uname -m 
```

## Detailed Steps

Docker includes an experimental feature called docker manifest. Please be aware the feature is experimental and not recommended for production use.

Docker manifest provides a different way of working. It allows separate images to be built for each architecture, which can be joined into a multi-arch image when it's time to share. This enables me to build and test on any architecture and postpone using multi-arch until later. When it's time to share a multi-arch image, it can be created in seconds using docker manifest. Docker manifest also makes it easy to update one of the architectures without emulation or remote builders.

### Build a simple Dockerfile to print the machine architecture

Create a new directory and save the two lines below into a file called Dockerfile 
```dockerfile
FROM ubuntu:latest
CMD echo -n "Architecture is " && uname -m
```

Docker image names have the form **repository/image-name:tag** 

Build the docker image using docker build, and attach the current architecture as the tag of the image. This will identify which architecture the image was created on.


```console 
arch=`uname -m` 
docker build -t jasonrandrews/uname:$arch .
```

### Run the simple image 

Run the image to print the architecture. 

```console
docker run --rm uname:$arch 
```

Push the image for this architecture to Docker Hub.

```console
docker push jasonrandrews/uname:$arch
```

Next, ssh to another machine with a different architecture and do the same thing. Build and push the 2nd image to Docker Hub. Both images are in the same repository uname, but there is one for each architecture. 

The last step is to join the two tags into a single multi-architecture image as uname:latest.

If the two machines have architectures of aaarch64 and x86_64 use the docker manifest command to join them.

```console
docker manifest create jasonrandrews/uname:latest \
--amend jasonrandrews/uname:aarch64 \
--amend jasonrandrews/uname:x86_64

docker manifest push --purge jasonrandrews/uname:latest
```

The purge option is not needed the first time, but to update one of the images and update the multi-arch image it is needed.

After the manifest push, a new multi-arch image with the latest tag is available. Pulling uname:latest from either architecture now works, and a user doesn't need to pay attention to the computer they are using.

The experimental docker manifest command offers a way to create multi-architecture images by joining multiple images using a manifest. Docker manifest provides additional features not covered here, and is useful to create, inspect, and modify manifest lists. 

[<-- Return to Learning Path](/cloud/docker/#sections)
