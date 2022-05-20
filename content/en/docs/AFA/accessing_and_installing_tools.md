---
tags: ["software tools"]
title: "Accessing and installing the Development Tools supplied with Arm Flexible Access"
linkTitle: "Installing Development Tools"
date: 2022-05-16
description: >
   Arm Development Tools are provided as Arm Success Kits. This article will help you download and install the appropriate components, and set up your tools license.
---
## Arm Success Kits

Arm Flexible Access (AFA) provides development tools packaged as [Arm Success Kits](https://www.arm.com/products/development-tools/success-kits). These come in two forms:

- Software Success Kits (SSK)
- Hardware Success Kits (HSK)

The exact number of licenses for each Success Kit you will have will depend on your AFA program membership. Please contact your AFA administration team or Arm account manager if you need confirmation.

Software Success Kits contain all of the tools Arm provides for developing and running code for your target.\
Hardware Success Kits are a super-set of Software Success Kits, adding tools for enabling architecture exploration, IP configuration, and system debug.

For more information on the contents of these kits see [this link](/docs/afa/which_tools)

**Note that as an AFA menber, you are also entitled to make use of [Arm IP Explorer](https://www.arm.com/products/ip-explorer). This is covered in a separate article.**

## Downloading Success Kit components {#download}

All AFA downloads are provided via the [Arm Product Download Hub](https://developer.arm.com/downloads). You will need to set up an account for this system to be able to download. It may be that only certain contacts within your organization have such access. If you are unsure, please contact your Arm account manager for assistance.

You can download individual components, or the complete success kits. Bundles are provided for Windows, Linux, or Mac OS. Note however that not all components are supported on all hosts.

The Product Download Hub uses [IBM Aspera Connect](https://www.ibm.com/aspera/connect/) to enable high-speed download of IP bundles. If prompted, follow on-screen instructions to install Aspera to your browser.

Once downloaded, you can untar the bundles, and install the necessary components.

## User Based License setup {#license}

All Arm tools are license managed. Arm is migrating all tools to a User Based Licensing (UBL) system which greatly simplifies license configuration. With a UBL license you have unlimited access to all components within the success kit you have enabled. The license is cached locally for up to 30 days, enabling remote or traveling users to have access to tools without connecting to their internal network. Using any component whilst connected to the network will renew the 30 days of license (this check is performed once per day upon the first use of the tools that day).

### Internal UBL server

The most common deployment method is to provide your AFA administration team with licenses to set up a UBL server for your organization. Contact your AFA administration team if you are unsure of the URL of the server.

Once this is running, to enable usage of the tools, go to the bin directory of any success kit component you have installed, and enter a command of the form:

- HSK: `armlm activate --server https://internal.ubl.server --product HWSKT-xxxx`
- SSK: `armlm activate --server https://internal.ubl.server --product SWSKT-xxxx`

To confirm you have enabled the license, enter the command:

`armlm inspect`

You now have access to all components within the success kit you have enabled. If you only require access to the components of SSK, it is strongly recommended that you only use an SSK license.

### Cloud based UBL server

In some cases you may have access to a cloud based UBL server, which you can enable with a supplied code. Contact your AFA adminstration team or Arm account manager if you are unsure what your code is.

`armlm activate --code xxxxxxxx-xxxx-xxxx-xxxxxxxx`

## Legacy FlexLM license setup

Users who do not yet have access to UBL licenses will have FlexLM licenses. You should set the environment variable `ARMLMD_LICENSE_FILE` to map to the location of your license server. Contact your AFA adminstration team for information on your internal license server. Arm expects all FlexLM licenses to be removed from AFA programs by end of 2023.

`export ARMLMD_LICENSE_FILE port@hostname`
