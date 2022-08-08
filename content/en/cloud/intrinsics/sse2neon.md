---
processors : ["Neoverse-N1"]
tools : ["gcc", "g++"]
software : ["linux"]
title: "Use sse2neon to port intrinsics to Neoverse"
linkTitle: "Use sse2neon to port intrinsics to Neoverse"
type: docs
weight: 2
hide_summary: true
description: >
    Port the example application to Arm Neoverse using sse2neon
---

The [sse2neon project](https://github.com/DLTcollab/sse2neon) is a quick way to get C/C++ applications compiling and running on Neoverse. The sse2neon header file provides NEON implementations for x64 intrinsics so no source code changes are needed. 

Each function call (intrinsic) is simply replaced with NEON instructions and will just work on Neoverse. 

To make this application compile and run on Neoverse there are three steps.

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

Assuming the new file is renamed to be neon.cpp this version can be compiled and run on the Arm architecture using the commands below. The g++ options are those recommended for Neoverse-N1.

```console
wget https://raw.githubusercontent.com/DLTcollab/sse2neon/master/sse2neon.h
g++ -O2 -march=armv8.2-a+fp16+rcpc+dotprod+crypto --std=c++14 neon.cpp -o neon
./neon
```
The program output is:

```console
result equals 6,8,10,12
```


[Proceed to the next Section -->](/cloud/intrinsics/simde)

[<-- Return to Learning Path](/cloud/intrinsics/#sections)

