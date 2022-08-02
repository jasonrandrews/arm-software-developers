---
processors : ["Neoverse-V1", "Neoverse-N1", "Neoverse-N2"]
software: ["linux"]
title: "Debugging with Arm DDT"
linkTitle: "Debugging with Arm DDT"
type: docs
hide_summary: true
description: >
    Tutorial on how to build an application for debugging and use the Arm DDT debugger
---

## Build for debugging

Edit the file in `src/make.def` and change the following line to disable compiler optimizations and add debugging symbols:

```console
CFLAGS = -O0 -g
```

## Build

Select your version C/Fortran/Python of the application in `src`, then build the application with:

```console
make
```

### Debug

In the same folder previously selected, run the C/Fortran application in parallel with:

```console
ddt mpirun -n 8 ./mmult
```

or using Python

```console
ddt mpirun -n 8 python ./mmult.py
```

Play the application in the debugger and investigate the reason for the crash.
