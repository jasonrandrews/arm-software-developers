---
processors : ["Neoverse-V1", "Neoverse-N1", "Neoverse-N2"]
software: ["linux"]
title: "Debug your application"
linkTitle: "Debug your application"
type: docs
hide_summary: true
description: >
    Tutorial on how to build an application for debugging and use the Arm DDT debugger
---

## Build options for debugging

Edit the file in `src/make.def` and change the following line to disable compiler optimizations and add debugging symbols:

```console
CFLAGS = -O0 -g
```

### Enable address sanitizer

To check for memory issues such as out-of-bound array accesses, you can enable the compiler's address sanitizer:

```console
CFLAGS = -O0 -g -fsanitize=address
```

## Build

Select your version C/Fortran/Python of the application in `src`, then build the application with:

```console
make
```

## Run

Select your version C/Fortran/Python of the application in `src`, then run the application with:

```console
mpirun ./mmult
```

or using Python

```console
mpirun python ./mmult.py
```

The matrix size can be set with an extra argument, e.g.

```console
mpirun ./mmult 1024
```

or using Python

```console
mpirun python ./mmult.py -s 1024
```

If you have enabled the compiler's address sanitizer, a report will be output when the application terminates. Look out for ERROR messages reporting out-of-bounds array accesses.


### Use a parallel debugger

To control the parallel execution and visualize the source code, a parallel debugger such as Arm DDT can help. 

In the same folder previously selected, run the C/Fortran application in parallel with:

```console
ddt mpirun ./mmult
```

or using Python

```console
ddt mpirun python ./mmult.py
```

This command will launch a GUI. Control options enable to run the application and investigate the bug.

## Fix the application

To fix the application, you can apply the following patch.

<script src="https://gist.github.com/armflorentlebeau/18e09268480a1453c0f31609138eae0b.js"></script>

## Next Steps

You are now ready to [profile and optimize the application](/hpc/get_started_mpi/profile).

[<-- Return to Learning Path](/hpc/get_started_mpi/#sections)
