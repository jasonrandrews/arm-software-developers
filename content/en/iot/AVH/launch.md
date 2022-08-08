---
title: "Launch an Arm Virtual Hardware instance in the cloud"
linkTitle: "Launch AVH instance"
type: docs
toc_hide: true
hide_summary: true
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
## Other connections {#other}

SSH connection creates a terminal to interact with the AVH instance. You can also interact through [other methods](https://arm-software.github.io/AVH/main/infrastructure/html/run_ami_local.html#other).

### Enable Code Server (Visual Studio Code)  {#vscode}
To enabling access to Visual Studio Code with a web browser, you will need to start a SSH tunnel to the instance and forward port `8080`.

```console
ssh -i <key.pem> -N -L 8080:localhost:8080 ubuntu@<AMI_IP_addr>
```
You can then access the IDE via a web browser on your local machine at:
```console
http://localhost:8080
```

### Enable Virtual Network Computing (VNC) {#vnc}

In the AVH terminal, enable and set VNC password (You do not need to enter a view-only password when prompted):
```console
vncpasswd
```
Start the VNC server for the session:
```console
sudo systemctl start vncserver@1.service
```
On your local machine, forward port `5901`.
```console
ssh -I <key.pem> -N –L 5901:localhost:5901 ubuntu@<AMI_IP_addr>
```
Connect your VNC client to port `5901`. You will be prompted for the VNC password.

## Next Steps

You are now ready to [build and run your first example](/iot/avh/microspeech)

[<-- Return to Learning Path](/iot/avh/#sections)
