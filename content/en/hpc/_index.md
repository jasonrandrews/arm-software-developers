
---
title: "High performance computing"
type: docs
description: >
    This section high performance computing on Arm.
weight: 30
---

{{% pageinfo %}}
Arm is at the center of the world’s largest compute ecosystem. The vast community of software, tools, and partners support and enable the use of Arm technology across a variety applications.

Our goal is to help developers find and use the platforms, tools, software and technical content.

We welcome community participation to continuously improve software development for the Arm architecture.
{{% /pageinfo %}}

{{< cardpane >}}
{{< card header="**Compilers**" >}}
Here is a list of compilers for HPC supporting C/C++, Fortran and OpenMP for multi-threading. These compilers support the latest Arm Neoverse processors and SVE extensions.
- Arm Compiler for Linux
    - [Install Arm Compiler for Linux](/compilers/install_acfl/)
    - [More information](https://developer.arm.com/Tools%20and%20Software/Arm%20Compiler%20for%20Linux)
- GNU GCC
    - [Install native GCC compiler on Linux](/compilers/install_ngcc/)
- GNU Fortran
    - [Install native Gfortan compiler on Linux](install_gfortran/)
{{< /card >}}
{{< card header="**MPI frameworks**" >}}
MPI is a message-passing interface standard for distributed computing:
- OpenMPI
- MPICH
{{< /card >}}
{{< card header="**HPC libraries**" >}}
HPC applications often rely on libraries providing common math operations, with C and Fortran interfaces: 
- OpenBLAS
- FFTW
- Arm Performance Libraries (includes BLAS, LAPACK and FFT interfaces)
{{< /card >}}
{{< card header="**Tools**" >}}
Scalable tools are necessary to debug or profile parallel applications:
- [Arm Forge](get_started_forge)
{{< /card >}}
{{< /cardpane >}}