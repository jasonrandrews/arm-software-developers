---
title: "Getting Started with Arm Forge"
linkTitle: "Getting Started with Arm Forge"
type: docs
weight: 5
hide_summary: true
description: >-
     This article describes how to install and use Arm Forge on a simple parallel application.
---

## Learning Objectives

By the end of this learning path, you will be able to:

- Debug and fix a parallel application with Arm DDT
- Profile and optimize with Arm MAP
- Use optimized BLAS routines with Arm Performance Libraries

The tutorial is available on [github](https://github.com/armflorentlebeau/arm_hpc_tools_trial). You can clone the repository with:

```console
git clone https://github.com/armflorentlebeau/arm_hpc_tools_trial
```

## Prequisites

To run the tutorial, you will need to install the following tools. Badges indicate the latest tested configuration on Arm v8-A:

|           | C   | Fortran | Python |
| ---       | --- | ---     | ---    |
| Compiler  | ![c_compiler](https://raw.githubusercontent.com/armflorentlebeau/arm_hpc_tools_trial/master/.github/badges/gcc.svg) | ![f_compiler](https://raw.githubusercontent.com/armflorentlebeau/arm_hpc_tools_trial/master/.github/badges/gfortran.svg) | ![python](https://raw.githubusercontent.com/armflorentlebeau/arm_hpc_tools_trial/master/.github/badges/python.svg) ![numpy](https://raw.githubusercontent.com/armflorentlebeau/arm_hpc_tools_trial/master/.github/badges/numpy.svg) |
| MPI       | ![openmpi](https://raw.githubusercontent.com/armflorentlebeau/arm_hpc_tools_trial/master/.github/badges/openmpi.svg) | ![openmpi](https://raw.githubusercontent.com/armflorentlebeau/arm_hpc_tools_trial/master/.github/badges/openmpi.svg) | ![mpi4py](https://raw.githubusercontent.com/armflorentlebeau/arm_hpc_tools_trial/master/.github/badges/mpi4py.svg) |
| BLAS      | ![blas](https://raw.githubusercontent.com/armflorentlebeau/arm_hpc_tools_trial/master/.github/badges/blas.svg) | ![blas](https://raw.githubusercontent.com/armflorentlebeau/arm_hpc_tools_trial/master/.github/badges/blas.svg) | ![scipy](https://raw.githubusercontent.com/armflorentlebeau/arm_hpc_tools_trial/master/.github/badges/scipy.svg) |
| Arm Forge | ![forge](https://img.shields.io/badge/forge-22.0.2-blue) |

## Sections

|          Type | Content                                    | Test |
| ---           | ---                                        | ---  |
| Tutorial      | [Build for debugging and fix](/hpc/get_started_forge/debug)       | ![c_debug](https://raw.githubusercontent.com/armflorentlebeau/arm_hpc_tools_trial/master/.github/badges/c_dbg.svg) ![f_debug](https://raw.githubusercontent.com/armflorentlebeau/arm_hpc_tools_trial/master/.github/badges/f_dbg.svg) ![py_debug](https://raw.githubusercontent.com/armflorentlebeau/arm_hpc_tools_trial/master/.github/badges/py_dbg.svg) |
| Tutorial      | [Build for profiling and optimize](/hpc/get_started_forge/profile)  | ![c_profile](https://raw.githubusercontent.com/armflorentlebeau/arm_hpc_tools_trial/master/.github/badges/c_prof.svg) ![f_profile](https://raw.githubusercontent.com/armflorentlebeau/arm_hpc_tools_trial/master/.github/badges/f_prof.svg) ![py_profile](https://raw.githubusercontent.com/armflorentlebeau/arm_hpc_tools_trial/master/.github/badges/py_prof.svg) |

## Download Arm Forge

## Installation {#install}
