---
tags: ["software tools"]
title: "Accessing and installing Success Kit components"
linkTitle: "Success Kit setup"
type: docs
toc_hide: true
hide_summary: true
weight: 30
description: >
   Arm Development Tools are provided as Arm Success Kits. This article will help you download and install the appropriate components, and set up your tools license.
---
## Arm Success Kits

Arm Flexible Access (AFA) provides development tools packaged as [Arm Success Kits](https://www.arm.com/products/development-tools/success-kits). These come in two forms:

- Software Success Kits (SSK)
- Hardware Success Kits (HSK)

For more information on the contents of these kits see [this link](/successkits)

## Downloading Success Kit components {#download}

All downloads are provided via the [Arm Product Download Hub](https://developer.arm.com/downloads). You will need to set up an account for this system to be able to download. It may be that only certain contacts within your organization have such access. If you are unsure, please contact your Arm account manager for assistance.

You can download individual components, or the complete success kits. Bundles are provided for Windows, Linux, or Mac OS. Note however that not all components are supported on all hosts.

The Product Download Hub uses [IBM Aspera Connect](https://www.ibm.com/aspera/connect/) to enable high-speed download of IP bundles. If prompted, follow on-screen instructions to install Aspera to your browser.

Once downloaded, you can untar the bundles, and install the necessary components.

For more information, see the [Getting Started Guide](https://developer.arm.com/documentation/107572).

## User Based License setup {#license}

All Arm tools are license managed. Arm is migrating all tools to a User Based Licensing (UBL) system which greatly simplifies license configuration. With a UBL license you have unlimited access to all components within the success kit you have enabled. The license is cached locally for up to 30 days, enabling remote or traveling users to have access to tools without connecting to their internal network. Using any component whilst connected to the network will renew the 30 days of license (this check is performed once per day upon the first use of the tools that day).

Full documentation is available for:
 - [License administration](https://developer.arm.com/documentation/107573)
 - [End user configuration](https://developer.arm.com/documentation/102516)

### Internal UBL server

The most common deployment method is to set up a UBL server for your organization.

Once this is running, to enable usage of the tools, go to the bin directory of any success kit component you have installed, and enter a command of the form:

- HSK:
```console
armlm activate --server https://internal.ubl.server --product HWSKT-STD0
```
- SSK:
```console
armlm activate --server https://internal.ubl.server --product SWSKT-STD0
```

To confirm you have enabled the license, enter the command:
```console
armlm inspect
```

You now have access to all components within the success kit you have enabled. Note that HSK is a super-set of SSK. If you only require access to the components of SSK, it is strongly recommended that you only use an SSK license.

Full license server setup and administation documentation is available below:
 - [Administrator](https://developer.arm.com/documentation/107573)
 - [End user](https://developer.arm.com/documentation/102516)


### Cloud based UBL server

In some cases you may have access to a cloud based UBL server, which you can enable with a supplied code. Contact your AFA adminstration team or Arm account manager if you are unsure what your code is.
```console
armlm activate --code xxxxxxxx-xxxx-xxxx-xxxxxxxx
```
To confirm you have enabled the license, enter the command:
```console
armlm inspect
```

## Legacy FlexLM license setup

Users who do not yet have access to UBL licenses will have FlexLM licenses. You should set the environment variable `ARMLMD_LICENSE_FILE` to map to the location of your license server. Contact your AFA adminstration team for information on your internal license server. Arm expects all FlexLM licenses to be removed from AFA programs by end of 2023.

{{< tabpane code=true >}}
  {{< tab header="Windows" >}}
set ARMLMD_LICENSE_FILE=port@server
{{< /tab >}}
  {{< tab header="Linux" >}}
export ARMLMD_LICENSE_FILE=port@server
{{< /tab >}}
{{< /tabpane >}}

## Next Steps

[Get Started with Success Kits](/getstarted/)