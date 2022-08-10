---
processors : ["Neoverse-V1", "Neoverse-N1", "Neoverse-N2"]
software: ["linux"]
tools: ["GCC", "Gfortran", "Arm Compiler for Linux", "perf", "Arm MAP", "Arm Performance Libraries"]
title: "Optimize your code"
linkTitle: "Optimize your code"
type: docs
hide_summary: true
description: >
    Tutorial on how to build an application for profiling and use the Arm MAP profiler
---

## Build options for profiling

Edit the file in `src/make.def` and make sure the code is compiled with debugging symbols `-g`, e.g.:

```console
CFLAGS = -O0 -g
```

Note that `-O0` disables compiler optimizations.

## Build

Select your version C/Fortran/Python of the application in `src`, then build the application with:

```console
make
```

## Run and profile your application

Install the Linux perf tools, e.g. on Ubuntu:

```console
sudo apt-get install linux-tools-common linux-tools-generic linux-tools-`uname -r`
```

and profile with:

```console
perf stat mpirun ./mmult 1024
```

This will provide information on a few hardware counter events as well as the elapsed time. First, we are going to investigate the amount of cycles per instruction. If low (less than 1), this indicates inefficiency.

### Use a parallel profiler

In the same folder previously selected, run the C/Fortran application in parallel with:

```console
map mpirun ./mmult 1024
```

or using Python

```console
map mpirun python ./mmult.py -s 1024
```

This command will launch a GUI, and profiling result will be displayed as a timeline and annotated code.

## Enable compiler optimizations

Edit the file in `src/make.def` to turn compiler optimizations on and report on vectorized loops: 

{{< tabpane >}}
  {{< tab header="GNU" >}}
  CFLAGS = -Ofast -g -fopt-info-vec
  {{< /tab >}}
  {{< tab header="Arm Compiler for Linux" >}}
  CFLAGS = -Ofast -g -Rpass=vector
  {{< /tab >}}
{{% /tabpane %}}


Then, rebuild the application before profiling again:

```console
make clean && make
```

## Investigate cache misses

To go further, we can specify hardware counter events to collect. For example, we can investigate memory access issues with:

```console
perf stat -e cache-misses,cache-references mpirun ./mmult 1024
```

If this ratio is high, memory access may be suboptimal. We can annotate the code where cache misses happen with the following perf commands:

```console
perf record -e cache-misses mpirun ./mmult 1024
perf report
```

## Optimize memory accesses

This patch will help the application benefit from the CPU caches:

<script src="https://gist.github.com/armflorentlebeau/6d630e1e2ef44a6fa024c29ec8ecb00e.js"></script>

## Use optimized routines

Install BLAS libraries, e.g. on Ubuntu:

```console
sudo apt-get install libblas-dev
```

And apply this patch to use the optimized routine instead of the hand-written matrix multiplication.

<script src="https://gist.github.com/armflorentlebeau/3513eddcb67baaca8b930182c09fb88e.js"></script>

### Use Arm Performance Library

Download Arm Performance Library [here](https://developer.arm.com/downloads/-/arm-performance-libraries), and edit `src/make.def` before rebuilding the application:

```console
CFLAGS = -Ofast -g -I $ARMPL_INCLUDES
LDFLAGS = -L $ARMPL_LIBRARIES -larmpl
```

## Summary

The graphs below summarize the optimizations on the C version of the application, when using 1, 2 or 4 processes on AWS Graviton 2.

![Graph](https://raw.githubusercontent.com/armflorentlebeau/arm_hpc_tools_trial/master/.github/data/graph.png)

## Next Steps

We have optimized the compute kernel of this example and we have new bottlenecks. Optimized versions of the application don't scale as we increase the number of processes. Because data transfers and IO are now dominant in the application, using more processors to compute the workload doesn't reduce the execution time linearly.

[<-- Return to Learning Path](/hpc/get_started_mpi/#sections)
