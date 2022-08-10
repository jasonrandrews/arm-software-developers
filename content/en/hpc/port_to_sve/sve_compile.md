---
processors : ["Neoverse-V1", "Neoverse-N2"]
software: ["linux"]
title: "Compile for SVE"
linkTitle: "Compile for SVE"
type: docs
hide_summary: true
description: >
    How to build code for SVE and useful compiler options.
---

## GNU

### C

```console
gcc -march=armv8-a+sve myapp.c -o myapp_c.out
```

### Fortran

```console
gfortran -march=armv8-a+sve myapp.f90 -o myapp_f90.out
```

### Autovectorization

With GCC autovectorization is enabled with the `-03` option. To disable autovectorization, use `-fno-tree-vectorize`.

Compare the output with autovectorization (left) and without (right):

<iframe width="1200px" height="800px" src="https://godbolt.org/e#g:!((g:!((g:!((h:codeEditor,i:(filename:'1',fontScale:14,fontUsePx:'0',j:1,lang:___c,source:'int+fun(double+*+restrict+a,+double+*+restrict+b,+int+size)%0A%7B%0A++for+(int+i%3D0%3B+i+%3C+size%3B+%2B%2Bi)%0A++%7B%0A++++b%5Bi%5D+%2B%3D+a%5Bi%5D%3B%0A++%7D%0A%7D'),l:'5',n:'0',o:'C+source+%231',t:'0')),k:30.548302872062667,l:'4',n:'0',o:'',s:0,t:'0'),(g:!((h:compiler,i:(compiler:carm64g1210,filters:(b:'0',binary:'1',commentOnly:'0',demangle:'0',directives:'0',execute:'1',intel:'0',libraryCode:'0',trim:'1'),flagsViewOpen:'1',fontScale:14,fontUsePx:'0',j:1,lang:___c,libs:!(),options:'-O3+-march%3Darmv8-a%2Bsve+-fno-tree-vectorize+',source:1,tree:'1'),l:'5',n:'0',o:'ARM64+gcc+12.1+(C,+Editor+%231,+Compiler+%231)',t:'0'),(h:compiler,i:(compiler:carm64g1210,filters:(b:'0',binary:'1',commentOnly:'0',demangle:'0',directives:'0',execute:'1',intel:'0',libraryCode:'0',trim:'1'),flagsViewOpen:'1',fontScale:14,fontUsePx:'0',j:2,lang:___c,libs:!(),options:'-O3+-march%3Darmv8-a%2Bsve',source:1,tree:'1'),l:'5',n:'0',o:'ARM64+gcc+12.1+(C,+Editor+%231,+Compiler+%232)',t:'0'),(h:diff,i:(fontScale:14,fontUsePx:'0',lhs:2,lhsdifftype:0,rhs:1,rhsdifftype:0),l:'5',n:'0',o:'Diff+Viewer+ARM64+gcc+12.1+vs+ARM64+gcc+12.1',t:'0')),k:69.45169712793732,l:'4',n:'0',o:'',s:2,t:'0')),l:'2',n:'0',o:'',t:'0')),version:4"></iframe>

Note the use of double-word register _d0_, _d1_ when disabling vectorization instead of SVE registers _z0.d_ and _z1_.

### Compiler insights

With GCC, the option `-fopt-info-vec` returns what loops were vectorized. To return what loop failed to vectorize, use `-fopt-info-vec-missed`.

<iframe width="1200px" height="800px" src="https://godbolt.org/e#g:!((g:!((g:!((h:codeEditor,i:(filename:'1',fontScale:14,fontUsePx:'0',j:1,lang:___c,source:'int+fun(double+*+restrict+a,+double+*+restrict+b,+int+size)%0A%7B%0A++for+(int+i%3D0%3B+i+%3C+size%3B+%2B%2Bi)%0A++%7B%0A++++b%5Bi%5D+%2B%3D+a%5Bi%5D%3B%0A++%7D%0A%7D'),l:'5',n:'0',o:'C+source+%231',t:'0')),k:19.937205651491368,l:'4',n:'0',o:'',s:0,t:'0'),(g:!((h:compiler,i:(compiler:carm64g1210,filters:(b:'0',binary:'1',commentOnly:'0',demangle:'0',directives:'0',execute:'1',intel:'0',libraryCode:'0',trim:'1'),flagsViewOpen:'1',fontScale:14,fontUsePx:'0',j:1,lang:___c,libs:!(),options:'-O3+-march%3Darmv8-a%2Bsve+-fopt-info-vec+',source:1,tree:'1'),l:'5',n:'0',o:'ARM64+gcc+12.1+(C,+Editor+%231,+Compiler+%231)',t:'0')),k:24.13927285458632,l:'4',n:'0',o:'',s:0,t:'0'),(g:!((h:output,i:(compilerName:'ARM64+gcc+12.1',editorid:1,fontScale:14,fontUsePx:'0',j:1,wrap:'1'),l:'5',n:'0',o:'Output+of+ARM64+gcc+12.1+(Compiler+%231)',t:'0')),k:55.923521493922316,l:'4',n:'0',o:'',s:0,t:'0')),l:'2',n:'0',o:'',t:'0')),version:4"></iframe>

Note that the compiler reports the vectorization of the loop line 3.

### Use Arm Performance Libraries

The Arm Performance Libraries include generic and target-specific SVE optimizations of common math operations used in HPC. To link your application with the libraries and GCC, use the predefined environment variables ARMPL_INCLUDES and ARMPL_LIBRARIES set by the Arm Performance Libraries module files provided:

```console
gcc -O3 -march=armv8-a+sve -I $ARMPL_INCLUDES dgemm.c -o dgemm.out -L $ARMPL_LIBRARIES -larmpl
```

## Arm Compiler for Linux

### C

```console
armclang -march=armv8-a+sve myapp.c -o myapp_c.out
```

### Fortran

```console
armflang -march=armv8-a+sve myapp.f90 -o myapp_f90.out
```

### Compiling for a specific SVE target with Arm Compiler for Linux

When compiling on the SVE-capable target, you can use `-march=native`. Otherwise, the following options are also available:
```console
-mcpu=neoverse-v1
-mcpu=neoverse-n2
-mcpu=a64fx
```

### Autovectorization

With Arm Compiler for Linux autovectorization is enabled with the `-02` option and above. To disable autovectorization, use `-fno-vectorize`.

### Compiler insights

With Arm Compiler for Linux, the option `-Rpass=vector` and `-Rpass=sve-loop-vectorize` return what loops were vectorized. To return what loop failed to vectorize, use `-Rpass-missed=vector`.

### Use Arm Performance Libraries

Using the Arm Performance Libraries with Arm Compiler for Linux is straightforward: the flag `-armpl=sve` ensures the SVE version of the library is used.

```console
armclang -O3 -march=armv8-a+sve -armpl=sve dgemm.c -o dgemm.out
```

## Next Steps

TODO

[<-- Return to Learning Path](/hpc/port_to_sve/#sections)