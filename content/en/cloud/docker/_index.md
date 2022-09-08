---
title: "Learn how to use Docker" 
type: docs
hide_summary: true
weight: 9
description: >
    Learning path for single and multi-architecture Docker commands. 
---

## Learning Objectives 

By the end of this learning path, you will be able to:

* Run Docker build to build and run a container image on any computer supporting Docker
* Use Docker buildx for multi-architecture image builds
* Install binfmt on Linux to add multi-architecture support for buildx
* Perform a remote docker build on an Arm server
* Utilize Docker manifest for multi-architecture builds


## Pre-requisites

* Docker is installed on the machines being used. For information about the installation refer to [Installing Docker](/devops/docker)

## Sections

|          Type | Content                       |
| ---           | ---                                 |
| How-To        | [Docker build for single-architecture builds](/cloud/docker/build)       |
| How-To        | [Docker buildx for multi-architechture builds](/cloud/docker/buildx) |
| How-To        | [Install binfmt for multi-architecutre support on Linux](/cloud/docker/binfmt) |
| How-To        | [Perform Docker builds on a remote machine of a different architecture](/cloud/docker/remote) |
| How-To        | [Docker manifest for multi-architecture builds](/cloud/docker/manifest) |
| Check         | [Knowledge check and review](/cloud/docker/knowledgecheck)                        |


## References and Documentation

| Type          | Content             |
| ---           | ---                 |
| Documentation | [Docker documentation](https://docs.docker.com) |
| Documentation | [Docker buildx documentation](https://docs.docker.com/engine/reference/commandline/buildx)      |
| Documentation | [Docker manifest documentation](https://docs.docker.com/engine/reference/commandline/manifest) |
| Docker Blog   | [Additional blog by Docker on buildx](https://www.docker.com/blog/how-to-rapidly-build-multi-architecture-images-with-buildx)|




