---
processors: ["Neoverse-N1"]
softwares: ["linux"]
title: "Running MongoDB on Arm"
linkTitle: "Run MongoDB on Arm"
type: docs
hide_summary: true
description: >
    This article shows you how to install and run MongoDB Community Edition on differet flavors of AWS EC2 instances powered by Arm64 achitecture.
---

## Pre-requisites

* Amazon Web Services (AWS) Account 

## Detailed Steps

The latest released version of MongoDB Community Edition (5.0) is supported on the following Linux distributions:

* Amazon Linux 2
* RHEL/CentOS 8
* Ubuntu Versions - 20.04, 18.04

Refer to this [page](https://www.mongodb.com/docs/manual/administration/production-notes/#platform-support-matrix) for the complete platform support matrix 

### Install and Run MongoDB on Amazon Linux 2

Using your AWS Account, launch an Arm 64-bit EC2 instance running Amazon Linux 2.

Then run through [these steps](https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-amazon/) to install and run MongoDB on your chosed EC2 instance.

### Install and Run MongoDB on Ubuntu

Using your AWS Account, launch and Arm 64-bit EC2 instance running either Ubuntu versions 20.04 or 18.04.

Then run through [these steps](https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-ubuntu/) on your chosen EC2 instance.

### Install and Run MongoDB on Red Hat

Using your AWS Account, launch and Arm 64-bit EC2 instance running RHEL8.

Then run through [these steps](https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-red-hat/) on your chosen EC2 instance.

[<-- Return to Learning Path](/cloud/webservice/mongodb-lp/#sections)



