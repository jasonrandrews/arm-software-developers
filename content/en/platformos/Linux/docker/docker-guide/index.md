---
tags: ["docker","graviton", "raspberrypi"]
title: "Docker guide for Arm developers"
linkTitle: "Docker guide for Arm developers"
type: docs
weight: 1
description: >
    Learn more about using Docker on a variety of Arm platforms
---

Docker containers are everywhere, primarily because they run the same everywhere. Containers are used on all major operating systems, on all major computing architectures to build, share, and run software. 
As more and more of the world’s computing happens on the Arm architecture, developers are looking for resources to make container development and deployment as easy as possible. 

We start by walking you through installing and deploying Docker on a variety of target machines. We then demonstrate how to use Docker to build, share and run containers using the simple examples provided. 
We hope you find these ideas helpful.

### [Get Started](#docker-setup)

## Table of Contents

- [Setup](#docker-setup)
   - [Tool Requirements](#tool-requirements)
   - [Workstation](#target-workstation)
      - [Arm Windows 10 laptop](#install-docker-on-a-windows-10-on-arm-laptop)
      - [Arm Linux laptop](#install-docker-on-arm-linux-laptop)
      - [Arm Chromebooks](#install-docker-on-arm-chromebooks)
      - [Windows 10 on x86_64](#install-docker-on-windows-10-on-x86_64)
      - [Linux on x86_64](#install-docker-on-linux-on-x86_64)
   - [Cloud](#target-in-the-cloud)
      - [AWS Graviton](#aws-graviton)
   - [Edge](#target-at-the-edge)
      - [Raspberry Pi 3 or 4](#raspberry-pi-3-or-4)
- [Build and Run](#build-and-run) 
   - [Windows 10 on Arm laptop OR Arm Linux laptop OR Arm Chromebook with Linux](#windows-10-on-arm-laptop-or-arm-linux-laptop-or-arm-chromebook-with-linux)
   - [Windows 10/Linux on x86_64 laptop](#windows-10linux-on-x86_64-laptop)
      - [Build and Run local](#build-and-run-local)
      - [Build on Remote machine and Run local](#build-on-remote-machine-and-run-local)
   - [Use GitHub actions to build and push Arm-based docker images](#use-github-actions-to-build-and-push-arm-based-docker-images)
      - [Use buildx to build multi-architecture Arm images](#use-buildx-to-build-multi-architecture-arm-images)
      - [Use build with Arm self-hosted runner](#use-build-with-arm-self-hosted-runner)


# Docker Setup 

The setup section covers how to install and use docker on various types of machine that may be on your desk, in the cloud, or at the edge. 
Before we dive into the setup details for different machines, it is helpful to have an overview of [Tool Requirements](#tool-requirements).

## Table of Contents

- [Tool Requirements](#tool-requirements)
- [Target: Workstation](#target-workstation)
   - [Arm Windows 10 laptop](#install-docker-on-a-windows-10-on-arm-laptop)
   - [Arm Linux laptop](#install-docker-on-arm-linux-laptop)
   - [Arm Chromebooks](#install-docker-on-arm-chromebooks)
   - [Windows 10 on x86_64](#install-docker-on-windows-10-on-x86_64)
   - [Linux on x86_64](#install-docker-on-linux-on-x86_64)
- [Target: Cloud](#target-in-the-cloud)
   - [AWS Graviton](#aws-graviton)
- [Target: Edge](#target-at-the-edge)
   - [Raspberry Pi 3 or 4](#raspberry-pi-3-or-4)

***

### Tool Requirements

Depending on the operating system you're using, there are different Docker products available to download.

***Docker products***

- [Docker Desktop for Windows and Mac](https://www.docker.com/products/docker-desktop)
- [Docker Engine for Linux](https://www.docker.com/products/container-runtime)

***Docker Engine versions***

- The Stable channel gives you latest releases for general availability.
- The Test channel gives pre-releases that are ready for testing before general availability (GA). Replace get.docker.com with test.docker.com below to get the test version.

### Install Docker
Let's proceed now with the installation of Docker. The Docker for Linux install procedure covers a majority of the target devices.  

### Docker for Linux install procedure

Almost universal, this procedure works for many Linux distributions. 

```shell
$ curl -fsSL get.docker.com -o get-docker.sh
$ sudo sh get-docker.sh
$ sudo usermod -aG docker your-user
$ newgrp docker (if you don’t want to log out and back in)
$ docker run hello-world
```

***Identify the architecture of any machine***
```shell
$ uname -m
```

If this Linux Install procedure does not work for you, or if you're using a Windows 10 x86_64 machine please select a different target device and proceed from there:
- [Target: Workstation](#target-workstation)
   - [Windows 10 on Arm laptop](#install-docker-on-a-windows-10-on-arm-laptop)
   - [Arm Linux laptop](#install-docker-on-arm-linux-laptop)
   - [Arm Chromebooks](#install-docker-on-arm-chromebooks)
   - [Windows 10 on x86_64](#install-docker-on-windows-10-on-x86_64)
   - [Linux on x86_64](#install-linux-on-x86_64)
- [Target: Cloud](#target-in-the-cloud)
   - [AWS Graviton](#aws-graviton)
- [Target: Edge](#target-at-the-edge)
   - [Raspberry Pi 3 or 4](#raspberry-pi-3-or-4)

***

## Target: Workstation

### Install Docker on a Windows 10 on Arm laptop

***Example systems are:***

- Microsoft Surface Pro X
- Samsung Galaxy Book S
- Lenovo Flex 5G
- Acer Spin 7

***Prerequisites***

- Install WSL 2 on the Windows 10 on Arm laptop. 
- Install the Ubuntu 20.04 Linux distribution in WSL 2 from the Microsoft Store.

***[More information available here](https://dev.to/aws-builders/windows-10-on-arm-with-wsl-2-2kbg)***

***Do it***

Use the general [Linux install procedure](#docker-for-linux-install-procedure)

```shell
$ sudo apt update 
$ curl -fsSL get.docker.com -o get-docker.sh
$ sudo sh get-docker.sh
$ sudo usermod -aG docker your-user
$ newgrp docker     (if you don’t want to log out and back in)
$ docker run hello-world
Docker daemon does not start automatically in WSL 2 but can be started manually:
$ sudo /etc/init.d/docker start
```

***How it works***

The Linux install will get the current docker release. [Review the script contents in a browser](https://get.docker.com/)

***More info***
- There are numerous Linux distribution options from the Microsoft Store.
- There is no Docker Desktop for Windows on Arm. Show your support for Docker Desktop on Arm [here](https://github.com/docker/roadmap/issues/91).
- For more information about [installing WSL 2](https://docs.microsoft.com/en-us/windows/wsl/install-win10)

***[Proceed to build and run instructions](#windows-10-on-arm-laptop-or-arm-linux-laptop-or-arm-chromebook-with-linux)***

***

### Install Docker on Arm Linux laptop

***Example systems are:***

- Pinebook Pro

***Prerequisites***

- Pinebook Pro laptop running Manjaro Arm

The almost universal Linux install doesn’t recognize Manjaro on Arm, but pacman will install docker.

***Do it***

Use the general [Linux install procedure](#docker-for-linux-install-procedure)

```shell
$ sudo pacman -Syu 
$ sudo pacman -S docker
$ sudo systemctl enable docker
$ sudo systemctl start docker
$ sudo usermod -aG docker your-user
$ newgrp docker     (if you don’t want to log out and back in)
$ docker run hello-world
```

***How it works***

The pacman install will get the current docker release.

***More info***

Nothing right now. 

***[Proceed to build and run instructions](#windows-10-on-arm-laptop-or-arm-linux-laptop-or-arm-chromebook-with-linux)***

***

### Install Docker on Arm Chromebooks

***Example systems are:***

- Acer Chromebook R13
- Lenovo Duet

***Prerequisites***

- Chromebooks can run Linux applications using the Linux feature. Go to the Chromebook Settings and enable Linux (Beta) feature. This will install the Linux subsystem, including a Debian 10 Buster distribution.
- Open the Linux terminal to use docker.

***Do it***

Use the general [Linux install procedure](#docker-for-linux-install-procedure)

```shell
$ sudo apt update 
$ curl -fsSL get.docker.com -o get-docker.sh
$ sudo sh get-docker.sh
$ sudo usermod -aG docker your-user
$ newgrp docker     (if you don’t want to log out and back in)
$ docker run hello-world
```

***[Proceed to build and run instructions](#windows-10-on-arm-laptop-or-arm-linux-laptop-or-arm-chromebook-with-linux)***

***

### Install Docker on Windows 10 on x86_64

***Prerequisites***

- Install Docker Desktop with WSL2 backend

***Do it***

- Follow [this procedure](https://docs.docker.com/docker-for-windows/wsl/) to download and install Docker Desktop for Windows
- Docker Desktop includes the buildx plugin by default

***More Info***

More information on the Docker Desktop on Windows [User Manual](https://docs.docker.com/docker-for-windows/).

***[Proceed to build and run instructions](#windows-10linux-on-x86_64-laptop)***

***

### Install Docker on Linux on x86_64

***Prerequisites***

- Docker on Linux 
- Docker buildx for multi-architecture image creation
- Instruction emulation(qemu) to register Arm executables to run on the x86 machine

***Do it***

- Use the general [Linux install procedure](#docker-for-linux-install-procedure) to install the latest verion 
- Install the instruction emulation to register Arm executables to run on the x86 machine 

```shell
$ docker run --rm --privileged docker/binfmt:820fdd95a9972a5308930a2bdfb8573dd4447ad3
```

***How it works***

- The docker/binfmt gets updated with the latest qemu and replaces any previous instructions that call for linuxkit/binfmt:v0.7

***More Info***

For more details [refer to the project](https://github.com/docker/binfmt)

***[Proceed to build and run instructions](#windows-10linux-on-x86_64-laptop)***

***

## Target: In the cloud

### AWS Graviton

***Prerequisites***

- Amazon Web Services (AWS) Account

***Do it***

Create and start an AWS-Graviton based EC2 instance

On the running AWS-Graviton based EC2 instance [Use the Linux install procedure](#docker-for-linux-install-procedure)

***More Info***

[Getting started guide in GitHub](https://github.com/aws/aws-graviton-getting-started/blob/master/containers.md )
[Get started with AWS Graviton-based EC2 instances](https://aws.amazon.com/ec2/graviton/)

***[Proceed to build and run instructions](#build-on-remote-machine-and-run-local)***

***

## Target: At the edge

### Raspberry Pi 3 or 4

***Do it***

[Use the Linux install procedure](#docker-for-linux-install-procedure)

***[Proceed to build and run instructions](#run-on-raspberry-pi-3-or-4)***

***



## Table of Contents
- [Windows 10 on Arm laptop OR Arm Linux laptop OR Arm Chromebook with Linux](#windows-10-on-arm-laptop-or-arm-linux-laptop-or-arm-chromebook-with-linux)
- [Windows 10/Linux on x86_64 laptop](#windows-10linux-on-x86_64-laptop)
   - [Build and run local](#build-and-run-local)
   - [Build on Remote machine and Run local](#build-on-remote-machine-and-run-local)
- [Use GitHub actions to build and push Arm-based docker images](#use-github-actions-to-build-and-push-arm-based-docker-images)
   - [Use buildx to build multi-architecture Arm images](#use-buildx-to-build-multi-architecture-arm-images)
   - [Use build with Arm self-hosted runner](#use-build-with-arm-self-hosted-runner)
- [Raspberry Pi 3 or 4](#run-on-raspberry-pi-3-or-4)
***

## Build and Run

This section covers how to build, share and run Docker containers for simple applications on various types of machine that may be on your desk, in the cloud, or at the edge.

### Windows 10 on Arm laptop OR Arm Linux laptop OR Arm Chromebook with Linux

Build a simple hello world example which prints the architecture of the machine. This is exactly the same on Windows 10 on Arm using WSL2, an Arm Linux laptop, or a Raspberry Pi 3 or 4 a running 64-bit operating system.

***Prerequisites***

- Get an example from git and select a language of interest. Choices are C, flask, golang, and PHP.

```shell
$ git clone https://github.com/jasonrandrews/hello-arm.git
$ cd hello-arm
```

***Do it***

***For the C language:***

```shell
$ cd c-hello-world
$ ./build.sh
$ ./run.sh
```

***How it works***

This is a local docker image build and run on a Windows 10 on Arm laptop using WSL. It looks just like Linux and will create an Arm image and run a container to print the architecture of the machine from the uname command. 

***

### Windows 10/Linux on x86_64 laptop

### Build and Run local

***Prerequisites***

A Docker ID to access [Docker Hub](https://hub.docker.com/) is required to push images to Docker Hub and share them.

Visit Docker Hub and create a new account using the [Sign up for Docker Hub](https://hub.docker.com/signup) link.

Once the account is created verify it can be used to login to Docker Hub.

Get the C language hello-world example

```shell
$ git clone https://github.com/pareenaverma/docker-projects
```

***Do it***

```shell
$ cd c-hello-world
```

Make sure to edit the build and run scripts to point to your Docker ID before running them.

```shell
$ ./build.sh
$ ./run.sh 
```

***How it works***

A multi-architecture docker image with the C application hello-world will be created and pushed to Docker Hub. The multi-architecture image is then run on either Windows 10/Linux x86_64 laptop, even if the container was also created for the Arm architecture.

***

### Build on Remote machine and Run local

***Prerequisites***

- Docker installed on remote AWS Graviton1/Graviton2 machine
- SSH-Key Authorization: SSH access to a remote docker host with a key-based authentication

***For local Linux machines:***
```shell
$ eval $(ssh-agent)
$ ssh-add <ssh-private-key>
```

***For local Windows machines:***
```shell
$ start-ssh-agent.cmd
$ ssh-add <ssh-private-key>
```

***Do it***

```shell
$ cd c-hello-world
```

Edit both remote-build.sh and local-run.sh to point to your Docker ID. Also edit remote-build.sh to point to the username and IP address of your AWS Graviton1/Graviton2 instance.

```shell
$ ./remote-build.sh
$ docker context use default
$./local-run.sh
```

***How it works***

An Arm architecture docker image with the C hello-world application is built on a remote machine. This image is pushed to Docker Hub. The image is then pulled from Docker Hub and run on a local machine.

***

### Use GitHub actions to build and push Arm-based docker images

#### Use buildx to build multi-architecture Arm images

***Prerequisites***

- A GitHub account
- A Docker Hub Account – a registry to push your image to
- A sample workflow and C language [hello world example](https://github.com/pareenaverma/docker-projects)

***Do it***

- Fork the https://github.com/pareenaverma/docker-projects repository
- The GitHub actions are in a specific directory .github/workflows
- Inspect the dockerbuildimg.yml file – this file contains the GitHub actions needed to build and push the Arm docker image for the c-hello-world to your Docker Hub account
- Edit the dockerbuildimg.yml file - change the DOCKER_IMAGE Docker ID to point to your Docker ID 
- Add the DOCKER_USERNAME and DOCKER_PASSWORD secrets to your GitHub repository. These point to your username and password of your DockerHub account.
   - Follow the steps under [“Creating encrypting secrets for a repository”](https://docs.github.com/en/free-pro-team@latest/actions/reference/encrypted-secrets) 
- Commit any simple change to your forked repository.
   - The example workflow is setup to trigger when you push code to your repository. 
- Go to the ‘Actions” menu on your repository to view the live actions when you commit a change.
- The Arm-docker image “c-hello-world-github" is built and pushed to the DockerHub registry. You can also log into Docker Hub and see your image pushed there.

***How it works***

The first step in the workflow is to check out the code from the repo, this will bring our codebase into our build environment for GitHub Actions. Then we pull in an Action which gives us the ability to run docker buildx. We then set some environment variables that are used by the docker commands. The next Action is to login into DockerHub with your encrypted secrets. Final step is running docker buildx to build/push our c-hello-world-github image into the DockerHub registry.

***

#### Use build with Arm self-hosted runner

The previous approach uses the GitHub runner to run the GitHub Actions. You can host your own runners and customize the environment used to run jobs in your GitHub Actions workflows. In this example we’ll detail how to build Arm-based Docker images with an Arm self-hosted runner in your GitHub Actions workflows.

***Prerequisites:***

- Linux Arm machine or AWS Graviton1/Graviton2 instance to be used as the self-hosted runner
- A GitHub account
- A Docker Hub Account – a registry to push your image to
- A sample workflow and C language [hello world example](https://github.com/pareenaverma/docker-projects)

***Do it***

- Fork [this repository](https://github.com/pareenaverma/docker-projects)
- Follow the steps under Adding a self-hosted runner to a repository. On step 5 select Operating System: Linux and Architecture: ARM64
- Follow the rest of the instructions to download, configure and run your self-hosted Arm runner
- Now inspect the ```.github/workflows/selfhostedrunner.yml``` file. This file contains the GitHub actions needed to build and push the Arm docker image for the c-hello-world to your Docker Hub account using the self-hosted runner.
- Add the ```DOCKER_USERNAME and DOCKER_PASSWORD``` secrets to your GitHub repository. These point to your username and password of your DockerHub account. Follow the steps under [“Creating encrypting secrets for a repository”](https://docs.github.com/en/free-pro-team@latest/actions/reference/encrypted-secrets) 
- Commit any simple change to your forked repository. The example workflow is setup to trigger when you push code to your repository.  Make sure your self-hosted runner is running.
- Go to the ‘Actions” menu on your repository to view the live actions when you commit a change.
- The Arm-docker image “c-hello-world" is built and pushed to the DockerHub registry. You can also log into Docker Hub and see your image pushed there.

#### Run on Raspberry Pi 3 or 4

Pull an existing Arm container from Docker Hub and run it on the Raspberry Pi 3 or Raspberry Pi 4.  

***Prerequisites:***

Docker is installed on the Raspberry Pi.  

***Do it***

```shell
$ docker pull jasonrandrews/c-hello-world 
$ docker run --rm -it c-hello-world 
```

***How it works***

The docker pull command will download the image from Docker Hub on to the local machine, and the docker run command will run it. The image was built on another Arm machine and runs seamlessly on the Raspberry Pi.  

