
---
title: "Performance analysis"
type: docs
description: >
    This section covers Performance Analysis tools
weight: 30
---

{{% pageinfo %}}
There are a few different profiling tools that you can use across a variety applications targeting Arm devices.

Our goal is to help developers find and use the the appropriate profiling tool for their application.

This page provides an overview of the available profiling tools, where to get them, and how to install and use them.
{{% /pageinfo %}}

{{< cardpane >}}
{{< card header="**[Arm Streamline Performance Analyzer](https://developer.arm.com/Tools%20and%20Software/Streamline%20Performance%20Analyzer)**" >}}
Arm Streamline Performance Analyzer is a commercial profiling tool for Android, Linux and bare-metal applications running on Arm processors.

Host machine support includes:
- Windows (x86)
- Linux (x86 and Arch64)
- MacOS (for profiling Android applications only) 

{{< /card >}}

{{< card header="**[perf]()**" >}}
perf is a performance analysis tool for Linux. It primarily uses the processor's performance counters but also gathers information from other sources to provide detailed statistics. The results from the tool can be used to understand and optimize the performance of your application. 

perf is available on all Linux distributions and can be installed using the package manager.

On Debian based distributions use:
```console
sudo apt install linux-tools-common linux-tools-generic linux-tools-`uname -r`
```

{{< /card >}}

{{< card header="**[Arm MAP](https://www.arm.com/products/development-tools/server-and-hpc/forge/map)**" >}}
Arm MAP, part of [Arm Forge](https://developer.arm.com/downloads/-/arm-forge), is a commercial parallel profiler for HPC applications on Linux. It supports all Arm Neoverse processors.

Supported languages:
- C/C++,
- Fortran,
- Python

Supported parallel programming standards:
- MPI,
- OpenMP,
- CUDA 
- OpenACC.
{{< /card >}}


{{< /cardpane >}}


