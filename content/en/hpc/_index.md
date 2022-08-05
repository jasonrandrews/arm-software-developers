---
title: "High performance computing"
type: docs
date: 2022-08-01T00:00:00+00:00
lastmod: 2022-08-05T00:00:00+00:00
description: >
    This section high performance computing on Arm.
weight: 30
---

{{% pageinfo %}}
Arm is at the center of the world’s largest compute ecosystem. The vast community of software, tools, and partners support and enable the use of Arm technology across a variety applications.

Our goal is to help developers find and use the platforms, tools, software and technical content.

We welcome community participation to continuously improve software development for the Arm architecture.
{{% /pageinfo %}}

## Learn
{{< cardpane >}}

<div class="card text-center">
  <div class="card-header" style="background-color:#95d600;">Introductory</div>
  <div class="card-body">
    <h5 class="card-title"> <b> Port code to SVE </b> </h5>
    <p class="card-text">
    <div style="text-align:left">
     <ul >
      <li>Understand the differences between SVE and NEON for vectorization</li>
      <li>Compile code for SVE-capable Arm processors</li>
      <li>Run SVE instructions on any Armv8-A processor</li>
     </ul>
    </div>
    </p>
    <a href="/hpc/port_to_sve" class="btn btn-primary">Learn More</a>
  </div>
  <div class="card-footer text-muted">Updated {{ $.Page.Lastmod.Format "January 02, 2006" }}</div>
</div>

<div class="card text-center">
  <div class="card-header" style="background-color:#95d600;">Introductory</div>
  <div class="card-body">
    <h5 class="card-title"> <b> Get started with parallel application development </b> </h5>
    <p class="card-text">
    <div style="text-align:left">
     <ul >
      <li>Debug and fix a parallel application</li>
      <li>Profile and optimize your code</li>
      <li>Use optimized routines for common math operations</li>
     </ul>
    </div>
    </p>
    <a href="/hpc/get_started_forge" class="btn btn-primary">Learn More</a>
  </div>
  <div class="card-footer text-muted">Updated {{ $.Page.Lastmod.Format "January 02, 2006" }}</div>
</div>

{{< /cardpane >}}

## Tools
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
{{< card header="**Development tools**" >}}
Scalable tools are necessary to debug or profile parallel applications:
- [Arm Forge](get_started_forge)
{{< /card >}}
{{< /cardpane >}}