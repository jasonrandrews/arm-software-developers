---
processors: ["Neoverse-N1"]
software: ["linux"]
title: "Install and Run MongoDB on Arm-based server"
linkTitle: "Run MongoDB on Arm"
type: docs
weight: 1
hide_summary: true
description: >
    Learn how to install and run MongoDB Community Edition on differet flavors of AWS EC2 instances powered by Arm64 achitecture.
---

## Pre-requisites

* An [Arm based instance](/cloud/platforms) from an appropriate cloud service provider

## Detailed Steps

The latest released version of MongoDB Community Edition (5.0) is supported on the following Linux distributions:

* Amazon Linux 2
* RHEL/CentOS 8
* Ubuntu Versions - 20.04, 18.04

Refer to this [page](https://www.mongodb.com/docs/manual/administration/production-notes/#platform-support-matrix) for the complete platform support matrix.

### Install and Run MongoDB on Ubuntu

Launch an Arm based instance from your cloud service provider, running Ubuntu versions 20.04 or 18.04.

Then run through [these steps](https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-ubuntu/) on your instance.

### Install and Run MongoDB on Red Hat

Launch an Arm based instance from your cloud service provider, running RHEL8.

Then run through [these steps](https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-red-hat/) on your instance.

### Install and Run MongoDB on Amazon Linux 2

Using your AWS Account, launch an Arm 64-bit EC2 instance running Amazon Linux 2.

Then run through [these steps](https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-amazon/) to install and run MongoDB on your chosed EC2 instance.

[<-- Return to Learning Path](/cloud/mongodb/#sections)
