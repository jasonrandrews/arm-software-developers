---
title: "Port Code to Arm SVE"
linkTitle: "Port Code to Arm SVE"
type: docs
hide_summary: true
weight: 10
description: >
    Learning path for porting code from NEON to the Arm Scalable Vector Extension (SVE).
---

## Learning Objectives

By the end of this learning path, you will be able to:

* Understand the differences between SVE and NEON for vectorization
* Compile code for SVE-capable Arm processors
* Run SVE instructions on any Armv8-A processor

## Pre-requisites

General knowledge about SIMD processing, vectorization or NEON.

## Sections

|          Type | Content                       |
| ---           | ---                                 |
| How-To        | [From NEON to SVE](/hpc/port_to_sve/sve_basics)       |
| How-To        | [Compile for SVE](/hpc/port_to_sve/sve_compile)       |
| How-To        | [Run SVE without capable hardware](/hpc/port_to_sve/sve_armie)       |
| Check         | [Knowledge check and review](knowledgecheck) |



## References and Documentation

| Type          | Content             |
| ---           | ---                 |
| Documentation | [Introduction to SVE](https://developer.arm.com/documentation/102476/latest/) |
| Documentation | [Arm Instruction Emulator user guide](https://developer.arm.com/documentation/102190/22-0/Get-started/Get-started-with-Arm-Instruction-Emulator) |
| Blog          | [Optimizing HPCG for Arm SVE](https://community.arm.com/arm-community-blogs/b/high-performance-computing-blog/posts/optimizing-hpcg-for-arm-sve) |

## Next Steps

HPC developers may be interested in [debugging](/ide) and [profiling](/perf) tools for SVE.

