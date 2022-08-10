---
date: 2018-10-06
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
  <div class="card-footer text-muted">Updated 5 August 2022</div>
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
    <a href="/hpc/get_started_mpi" class="btn btn-primary">Learn More</a>
  </div>
  <div class="card-footer text-muted">Updated 10 August 2022</div>
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
    - [Install native Gfortan compiler on Linux](/compilers/install_gfortran/)
{{< /card >}}
{{< card header="**MPI frameworks**" >}}
MPI is a message-passing interface standard for distributed computing:
- [OpenMPI](https://docs.open-mpi.org/en/v5.0.x/quickstart.html)
- [MPICH](https://www.mpich.org/)
{{< /card >}}
{{< card header="**HPC libraries**" >}}
HPC applications often rely on libraries providing common math operations, with C and Fortran interfaces: 
- [OpenBLAS](https://www.openblas.net/)
- [FFTW](https://www.fftw.org/)
- [Arm Performance Libraries](https://developer.arm.com/downloads/-/arm-performance-libraries) (includes BLAS, LAPACK and FFT interfaces)
{{< /card >}}
{{< card header="**Development tools**" >}}
Scalable tools help fixing and optimizing HPC applications:
- Parallel debugger: [Arm DDT](/ide/ddt)
- Parallel profiler: [Arm MAP](/perf/map)

Arm DDT and MAP are part of [Arm Forge](https://developer.arm.com/downloads/-/arm-forge).
{{< /card >}}
{{< /cardpane >}}