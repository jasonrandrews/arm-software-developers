---
title: "Installing GFortran on Linux"
linkTitle: "Installing GFortran on Linux"
type: docs
weight: 5
hide_summary: true
description: >-
     This article describes how to download and install GFortran for various Linux distributions.
---

## Introduction

The GCC toolchain is available on all Linux distributions. This section covers native gfortran on Arm Linux distributions.

To make sure you are using an Arm machine run the command

```console
uname -m
```

It should return
```console
aarch64
```

## Download 

The Linux package manager will download the required files so there are no special download instructions.

## Installation {#install}

### Installing on Debian based distributions such as Ubuntu

Use the `apt` command to install software packages on any Debian based Linux distribution.

```console
sudo apt update
sudo apt install gfortran
```

### Installing on Red Hat / Fedora / Amazon Linux

These Linux distributions use `yum` as the package manager. 

To install the most common development tools use the commands below. If the machine has `sudo` you can use it or run `yum` as _root_.

```console
sudo yum update
sudo yum groupinstall 'Development Tools'
```

If `sudo` is not available become _root_ and omit the `sudo`.

```console
yum update
yum groupinstall 'Development Tools'
```

## Setting up product license {#license}

Arm GNU Toolchain is open source and freely available for use. No licenses need to be set up for use.

## Get started {#start}

To confirm the installation is complete run:

```console
gfortran --version
```

To compile an example program, create a text file named hello-world.c with the contents below.

```fortran
program hello-world
  ! This is a comment line; it is ignored by the compiler
  print *, 'Hello, World!'
end program hello-world
```

To compile the hello-world program use:

```console
gfortran -o hello-world hello-world.f90
```

To run the application enter:

```console
./hello-world
```

The program will print the string in the printf() statement.

