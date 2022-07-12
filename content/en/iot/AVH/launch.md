---
title: "Launch an Arm Virtual Hardware instance in the cloud"
linkTitle: "Launch AVH instance"
type: docs
description: >
    How to launch an Arm Virtual Hardware instance in the cloud.
---
## Overview

Follow these instructions to launch an Arm Virtual Hardware instance in the cloud

## Pre-requisites

* Cloud service account
  - Amazon Web Services (AWS)

## Detailed Steps

### Log into your Cloud Service account

To help you get started, we are offering 100+ hours of free AWS EC2 CPU credits. These credits have been provided by AWS for the first 1,000 qualified users. To claim your credits, apply online [here](https://www.arm.com/company/contact-us/virtual-hardware).

### Locate Arm Virtual Hardware in your service provider marketplace

{{< tabpane code=true >}}
  {{< tab header="AWS" >}}
https://aws.amazon.com/marketplace/pp/prodview-urbpq7yo5va7g
{{< /tab >}}
{{< tab header="Others" >}}
Coming soon
{{< /tab >}}
{{< /tabpane >}}

### Subscribe to the service, and proceed to launch your AVH instance

{{< tabpane code=true >}}
  {{< tab header="AWS" >}}
A c5.large instance type is recommended
{{< /tab >}}
{{< tab header="Others" >}}
Coming soon
{{< /tab >}}
{{< /tabpane >}}

The instance requires that a key-pair be used for security. Other settings can be as default.

### Connect to instance terminal via SSH

On your local machine, run the following command to connect to the instance with user name `ubuntu`.
```console
ssh  -i <path>/your_key.pem ubuntu@<Public IPv4 address>
```
  * `-i` specifies the private key file specified when launching instance.
  * `<Public IPv4 address>` is the public IP address of the instance.

You can also connect via cloud service provider GUI, or terminal utilities such as [MobaXTerm](https://mobaxterm.mobatek.net/), [PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/), and others.

### Verify instance has launched successfully

In your SSH terminal, run the `tool-inventory.sh` script to verify the instance has launched successfully, and component tools are available for use.
```console
./tool-inventory.sh
```

## Next Steps

You are now ready to [build and run your first example](/iot/avh/microspeech)
