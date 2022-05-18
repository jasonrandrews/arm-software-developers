---
title: "Porting Architecture Specific C/C++ Intrinsics to Arm Neoverse"
linkTitle: "Porting Architecture Specific C/C++ Intrinsics to Arm Neoverse"
description: >
    Migrating C/C++ applications from x64 to Arm Neoverse requires recompiling the source code for the Arm architecture. The marketing message of a “simple recompile” works much of the time, but not always. SIMD extensions are one of the common barriers encountered when porting C/C++ applications from x64 to Arm Neoverse. Today, let’s look at what to do if you encounter architecture specific intrinsics when compiling for Arm Neoverse. We will start with a short background followed by a plan to get your code compiled and running.
---

**What are intrinsics?**

First, a little background about intrinsics. Intrinsics are functions which are built into the compiler and not part of a library. They look like function calls, but don’t require an actual function call. When the compiler encounters intrinsics it directly substitutes a sequence of instructions. Intrinsics are often used to access special instructions that don’t have a direct mapping from C/C++ or when performance optimization is needed. 

One use of intrinsics is to access SIMD (single-instruction, multiple-data) instructions directly from C/C++ for improved application performance. Intrinsics are easier to work with compared to assembly language, but they often pose a challenge when porting source code to a new architecture. This portability barrier is not very appealing if you were thinking a recompile was all that was needed. The situation may be worse if you are not familiar with the code.

Intel Streaming SIMD Extensions (SSE) and [Arm NEON](https://developer.arm.com/documentation/dht0002/a/Introducing-NEON/NEON-architecture-overview/NEON-instructions) SIMD instructions increase processor throughput by performing multiple computations with a single instruction. Over the years, Intel and Arm have introduced a variety of SIMD extensions. NEON is used in many of the Arm Cortex-R, Cortex-A, and Neoverse processors.

If you are not familiar with SIMD instructions there are numerous tutorials available. There are generally 3 ways to program SIMD hardware:

1. The C/C++ compiler recognizes opportunities to use SIMD instructions and inserts them automatically (with or without some guidance)
2. Intrinsics to access SIMD instructions directly from C/C++ source code
3. Assembly programming 

**What is sse2neon?**

The [sse2neon project](https://github.com/DLTcollab/sse2neon) is a quick way to get C/C++ applications compiling and running on Arm Neoverse. The sse2neon header file provides NEON implementations for x64 intrinsics so no source code changes are needed. Each function call (intrinsic) is simply replaced with NEON instructions and will just work on Arm Neoverse. 

Below is a small example which demonstrates the process of using sse2neon. The source code comes from a [short course titled Efficient Vectorisation with C++](https://chryswoods.com/vector_c++/emmintrin.html) and is copyright (C) Christopher Woods, 2006-2015 and is licensed under the [Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-nc-sa/4.0/).

```cpp
#include <iostream>

#ifdef __SSE2__
  #include <emmintrin.h>
#else
  #warning SSE2 support is not available. Code will not compile
#endif

int main(int argc, char **argv)
{
    __m128 a = _mm_set_ps(4.0, 3.0, 2.0, 1.0);
    __m128 b = _mm_set_ps(8.0, 7.0, 6.0, 5.0);

    __m128 c = _mm_add_ps(a, b);

    float d[4];
    _mm_storeu_ps(d, c);

    std::cout << "result equals " << d[0] << "," << d[1]
              << "," << d[2] << "," << d[3] << std::endl;

    return 0;
}
```

First, we see a reference to the \_\_SSE2\_\_ preprocessor define and the emmintrin.h header file. These are architecture specific extensions, the function calls starting with _mm are Intel SSE intrinsics.

Assuming the source code file name is sse.cpp the code above is compiled on the x64 architecture and run with the commands below.

```console
$ g++ -O2 -msse2 --std=c++14 sse.cpp -o sse
$ ./sse
```

To make this application compile and run on Arm Neoverse there are three steps.

1. Adjust the SSE specific header file usage for the Arm architecture
2. Include sse2neon.h to map the intrinsics to NEON instructions
3. Change the g++ compiler flags for the Arm architecture


Here is the new program. The only change is related to the include files.

```cpp
#include <iostream>

#ifdef __SSE2__
  #include <emmintrin.h>
#else
  #ifdef __aarch64__
    #include "sse2neon.h"
  #else
    #warning SSE2 support is not available. Code will not compile
  #endif
#endif

int main(int argc, char **argv)
{
    __m128 a = _mm_set_ps(4.0, 3.0, 2.0, 1.0);
    __m128 b = _mm_set_ps(8.0, 7.0, 6.0, 5.0);

    __m128 c = _mm_add_ps(a, b);

    float d[4];
    _mm_storeu_ps(d, c);

    std::cout << "result equals " << d[0] << "," << d[1]
              << "," << d[2] << "," << d[3] << std::endl;

    return 0;
}
```

Assuming the new file is renamed to be neon.cpp this version can be compiled and run on the Arm architecture using the commands below. The g++ options are those recommended for Arm Neoverse.

```console
$ g++ -O2 -march=armv8.2-a+fp16+rcpc+dotprod+crypto --std=c++14 neon.cpp -o neon
$ ./neon
```
In both cases the program output is:

```console
result equals 6,8,10,12
```

**What else is available to help with porting to Arm Neoverse?**

I always point people to [Getting started with AWS Graviton](https://github.com/aws/aws-graviton-getting-started) as a good place to find useful migration information and other helpful tips. 

Another tool which may be useful is [aarch64 Porting Advisor](https://github.com/arm-hpc/porting-advisor). It is a quick way to identify architecture specific code. Porting Advisor is not needed for the simple example presented above, but if there are architecture specific intrinsics hiding deep in a larger project it can help find them. 

To use Porting Advisor install it using the commands below.

```console
$ git clone https://github.com/arm-hpc/porting-advisor.git
$ cd porting-advisor
$ sudo python3 setup.py install
```

Run Porting Advisor by supplying the directory with the source code to be analyzed. For example, to try it on the open source KasmVNC project use the commands below.

```console
$ git clone https://github.com/kasmtech/KasmVNC.git
$ porting-advisor KasmVNC 
| Elapsed Time: 0:00:00                                                                                                              
413 files scanned.
KasmVNC/common/rfb/scale_sse2.cxx: 55 other issues
KasmVNC/common/rfb/scale_sse2.cxx:74 (SSE2_halve): architecture-specific intrinsic: _mm_loadu_si128
KasmVNC/common/rfb/scale_sse2.cxx:75 (SSE2_halve): architecture-specific intrinsic: _mm_loadu_si128
KasmVNC/common/rfb/scale_sse2.cxx:62 (SSE2_halve): architecture-specific intrinsic: _mm_set_epi32
KasmVNC/common/rfb/scale_sse2.cxx:63 (SSE2_halve): architecture-specific intrinsic: _mm_set_epi32
KasmVNC/common/rfb/scale_sse2.cxx:64 (SSE2_halve): architecture-specific intrinsic: _mm_set_epi32
KasmVNC/common/rfb/scale_sse2.cxx:61 (SSE2_halve): architecture-specific intrinsic: _mm_setzero_si128
KasmVNC/common/rfb/scale_sse2.cxx:78 (SSE2_halve): architecture-specific intrinsic: _mm_unpackhi_epi8
KasmVNC/common/rfb/scale_sse2.cxx:80 (SSE2_halve): architecture-specific intrinsic: _mm_unpackhi_epi8
KasmVNC/common/rfb/scale_sse2.cxx:77 (SSE2_halve): architecture-specific intrinsic: _mm_unpacklo_epi8
KasmVNC/common/rfb/scale_sse2.cxx:79 (SSE2_halve): architecture-specific intrinsic: _mm_unpacklo_epi8

Use --output FILENAME.html to generate an HTML report.
```

Porting Advisor scans the directory and immediately points out architecture specific extensions. Check out the usage instructions for more information.

**Summary**

Arm designed the Neoverse cores to deliver the best price performance for many workloads. Many developers have successfully migrated applications to Neoverse and were happy with the results. Architecture specific intrinsics are just one possible migration barrier, but one which can usually be overcome. 

Let us know what else is stopping you from migrating applications to Arm Neoverse processors. 


