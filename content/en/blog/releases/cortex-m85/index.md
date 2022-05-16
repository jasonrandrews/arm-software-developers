
---
title: "Cortex-M85 Support"
linkTitle: "Cortex-M85 Support"
date: 2022-04-26
description: >
    New tools for Cortex-M85 are avilable
resource:
- src: "**.jpeg"
---

## Arm Development Studio

[Cortex-M85](https://developer.arm.com/Processors/Cortex-M85) is the latest processor from Arm for embedded IoT and ML applications. Cortex-M85 is the most capable Cortex-M processor, with micro-architectural improvements to deliver best in class performance, and advanced security features, being the first processor to implement [Armv8.1-M Pointer Authentication and Branch Target Identification](https://community.arm.com/arm-community-blogs/b/architectures-and-processors-blog/posts/armv8-1-m-pointer-authentication-and-branch-target-identification-extension) (PACBTI-M).

Arm Development Studio 2022.0 provides complete support for Cortex-M85 in all (Bronze and higher) available editions. Arm Compiler for Embedded 6.18 allows users to build code optimized for the processor, as well as enabling developers to build code to [support PACBTI-M](https://developer.arm.com/documentation/100748/0618/Security-features-supported-in-Arm-Compiler-for-Embedded/Armv8-1-M-PACBTI-extension-mitigations-against-ROP-and-JOP-style-attacks). An example project highlighting these features is provided, which can be run on the supplied Fixed Virtual Platform, and debugged with the Arm Debugger.

{{< imgproc ds-m85 Fill "1122x488" >}}
{{< /imgproc >}}

Supported Tools
* Arm IP Explorer
* Arm DS 2022.0
* MDK 5.37
* CMSIS Core
