---
title: "Large System Extenstions (LSE)"
linkTitle: "Large System Extenstions (LSE)"
description: >
    Large System Extensions (LSE) improve the performance of atomic operations in systems with many processors. Understanding LSE helps developers port software applications to Arm Neoverse processors.
---

### Introduction

In programming, when multiple processors or threads access shared data, and at least one is writing, the operations must be atomic. This means the data accesses must be treated as a single operation relative to the other processors to avoid data race conditions. Microprocessors are designed to treat sequences such as read-modify-write and memory-register exchange as single operations, even when they create multiple accesses to memory. This hardware makes programming easier. 

The Armv8.1-A architecture introduced new atomic instructions. Atomics are alternatives to the load, store exclusive sequences used in previous architecture versions.

The [Arm Architecture Reference Manual](https://developer.arm.com/documentation/ddi0487/latest) refers to the atomic instructions as Large System Extensions (LSE). You may see them referred to as FEAT_LSE in documentation or in compiler information indicating support for the atomic instructions. 

From the Architecture Reference Manual, FEAT_LSE introduces a set of atomic instructions:

- Compare and Swap instructions, CAS and CASP
- Atomic memory operation instructions, LD and ST, where is one of ADD, CLR, EOR, SET, SMAX, SMIN, UMAX, and UMIN
- Swap instruction, SWP

Additional architecture improvements were made in Armv8.4-A and made optional in Armv8.2-A, but we won’t cover the low-level hardware details. This additional feature is referred to as FEAT_LSE2 in the Architecture Reference Manual.

In architecture versions prior to LSE, read-modify-write sequences use load exclusive and store exclusive instructions. Incrementing a shared variable uses a sequence such as:

**LDXR** to read current count (load exclusive)
**ADD** to add one to the shared variable
**STXR** to attempt to store to memory (store exclusive)
**CMP** to check if the operation succeeded

Because atomic accesses use multiple instructions each processor is required to implement an exclusive monitor. The exclusive monitor is a hardware state machine to track the read-modify-write sequences and match up the loads and stores. You can read about the exclusive monitor in the technical reference manual of a processor such as the [Cortex-A53](https://developer.arm.com/documentation/ddi0500/j/Level-1-Memory-System/L1-Data-memory-system/Internal-exclusive-monitor?lang=en).

If the number of processors is small, this works fine. Increasing processor counts combined with increased caching, make it hard to maintain fairness as processors closer to each other have a better chance of completing atomic sequences.

With LSE, atomic instructions provide a non-interruptible read-modify-write sequence in a single instruction. The atomic instructions can perform simple arithmetic or logical operations on the specified memory location, and return the updated value to the processor. Programmer’s benefit from the atomic instructions because it’s easier to specify a single instruction compared to a sequence of instructions with a loop around them if the sequence fails. 

Atomic instructions work better in situations such as networking software where many counters are atomically updated from many processors. The atomic instructions result in faster performance and less variability. 

With this introduction, let’s see how this applies to Arm Neoverse processors. 

### LSE in Arm Neoverse Processors

Let's use AWS as an exmaple of how to evaluate and understand LSE.

Today, AWS offers two generations of Graviton processors. The first instance type is A1, and was announced at re:Invent 2018. Announced at re:Invent 2019, Graviton2 processors provide a significant performance uplift from A1. The Graviton2 instance types are M6g, T4g, C6g, and R6g. C7g instances, powered by the latest generation AWS Graviton3 processors, were announced at re:Invent 2021 and developers can [request access](https://aws.amazon.com/ec2/graviton/) now. 
 
A1 instances are based on the Cortex-A72 processor. The Cortex-A72 implements the Armv8.0-A architecture and does not include the atomic instructions. All of the AWS EC2 instances based on the Neoverse-N1 processor, M6g, T4g, C6g, and R6g as well as the C7g include the atomic instructions. 

One of the common performance issues when migrating to Graviton2 is running software that does not utilize LSE. Software built with load exclusives and store exclusives usually runs slower on Graviton2 instances. 

Let’s look at how to make sure you get the best performance on Graviton2.

**How do I know if my Linux kernel supports atomics?**

There are a couple of ways to check. First, look in the kernel ring buffer messages to see if LSE is present.

```console
$ sudo dmesg | grep LSE
[    0.001296] CPU features: detected: LSE atomic instructions
```

Another way is to use the lscpu command to print the processor information. Look specifically at the flags (last item).

Here is the output from an AWS A1 instance:
```console
$ lscpu
Architecture:                    aarch64
CPU op-mode(s):                  32-bit, 64-bit
Byte Order:                      Little Endian
CPU(s):                          1
On-line CPU(s) list:             0
Thread(s) per core:              1
Core(s) per socket:              1
Socket(s):                       1
NUMA node(s):                    1
Vendor ID:                       ARM
Model:                           3
Model name:                      Cortex-A72
Stepping:                        r0p3
BogoMIPS:                        166.66
L1d cache:                       32 KiB
L1i cache:                       48 KiB
L2 cache:                        2 MiB
NUMA node0 CPU(s):               0
Vulnerability Itlb multihit:     Not affected
Vulnerability L1tf:              Not affected
Vulnerability Mds:               Not affected
Vulnerability Meltdown:          Not affected
Vulnerability Spec store bypass: Not affected
Vulnerability Spectre v1:        Mitigation; __user pointer sanitization
Vulnerability Spectre v2:        Mitigation; Branch predictor hardening
Vulnerability Srbds:             Not affected
Vulnerability Tsx async abort:   Not affected
Flags:                           fp asimd evtstrm aes pmull sha1 sha2 crc32 cpuid
```

Here is the output from an AWS T4g instance.

```console
$ lscpu
Architecture:                    aarch64
CPU op-mode(s):                  32-bit, 64-bit
Byte Order:                      Little Endian
CPU(s):                          2
On-line CPU(s) list:             0,1
Thread(s) per core:              1
Core(s) per socket:              2
Socket(s):                       1
NUMA node(s):                    1
Vendor ID:                       ARM
Model:                           1
Model name:                      Neoverse-N1
Stepping:                        r3p1
BogoMIPS:                        243.75
L1d cache:                       128 KiB
L1i cache:                       128 KiB
L2 cache:                        2 MiB
L3 cache:                        32 MiB
NUMA node0 CPU(s):               0,1
Vulnerability Itlb multihit:     Not affected
Vulnerability L1tf:              Not affected
Vulnerability Mds:               Not affected
Vulnerability Meltdown:          Not affected
Vulnerability Spec store bypass: Mitigation; Speculative Store Bypass disabled via prctl
Vulnerability Spectre v1:        Mitigation; __user pointer sanitization
Vulnerability Spectre v2:        Not affected
Vulnerability Srbds:             Not affected
Vulnerability Tsx async abort:   Not affected
Flags:                           fp asimd evtstrm aes pmull sha1 sha2 crc32 atomics fphp asimdhp cpu
                                 id asimdrdm lrcpc dcpop asimddp ssbs
```

For Neoverse-N1 the “atomics” flag is listed indicating LSE support.

**Which versions of the GCC compiler support LSE?**

LSE support started way back in GCC 6, but currently GCC 9 and GCC 10 are good to use.

**What are out-of-line atomics?**

When an atomic operation is encountered by the compiler, calls to helper functions that provide the best implementation for the processor are inserted instead of directly generating in-line instructions.

The gcc command line options -moutline-atomics and -mno-outline-atomics enable or disable calls to the out-of-line helpers. 

With GCC 9.3.1 and later, you can use the above options to enable/disable out-of-line atomics.

With GCC 10.1, out-of-line atomics are enabled by default. Refer to [Making the most of the Arm architecture with GCC 10](https://community.arm.com/arm-community-blogs/b/tools-software-ides-blog/posts/making-the-most-of-the-arm-architecture-in-gcc-10) for more info. 

**Which CPU or architecture version should I specify with gcc?**

In the [Graviton getting started](https://github.com/aws/aws-graviton-getting-started/blob/main/c-c++.md) on GitHub AWS recommends using
-march=armv8.2-a+fp16+rcpc+dotprod+crypto 
for GCC targeting Graviton2.

It’s generally a good idea to use the latest compiler available on the operating system being used.

**Is LSE built into the C library on my operating system?**

Yes, if you are using any of the operating systems below. Only Ubuntu 18.04 requires an extra package to be installed. 

- Amazon Linux 2
- Amazon Linux 2022
- Ubuntu 18.04 (needs `apt install libc6-lse`)
- Ubuntu 20.04
- Ubuntu 22.04

**How do I know if my compiler is generating LSE instructions?**

Let’s take a look at an example to get more understanding. 

Here is an [example program from cppreference.com](https://en.cppreference.com/w/c/language/atomic):

```cpp
#include <stdio.h>
#include <threads.h>
#include <stdatomic.h>
 
atomic_int acnt;
int cnt;
 
int f(void* thr_data)
{
    for(int n = 0; n < 1000; ++n) {
        ++cnt;
        ++acnt;
    }
    return 0;
}
 
int main(void)
{
    thrd_t thr[10];
    for(int n = 0; n < 10; ++n)
        thrd_create(&thr[n], f, NULL);
    for(int n = 0; n < 10; ++n)
        thrd_join(thr[n], NULL);
 
    printf("The atomic counter is %u\n", acnt);
    printf("The non-atomic counter is %u\n", cnt);
}
```
The atomic_int C data type is used to indicate that accesses to the acnt variable must be atomic.

Let’s start on an AWS A1 instance. This is Cortex-A72, without LSE.

**A1 Instance**

I’m using Ubuntu 20.04 and the default gcc version is 9.4.0:

```console
$ gcc --version
gcc (Ubuntu 9.4.0-1ubuntu1~20.04.1) 9.4.0
Copyright (C) 2019 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
```

Save the above C program as atomic.c and compile the application:

```console
$ gcc -g atomic.c -o a1 -march=armv8-a -lpthread
$ objdump -S a1 > a1.dis
```

Review the file a1.dis and check the instructions for incrementing acnt. The sequence is:

- Address of acnt is loaded into x0
- Value of acnt is loaded into w1 using load exclusive
- Add 1 to acnt
- Store exclusive to write the new value
- Check if the store succeed and if not loop back to 0x998 and load again

Here is the disassembly:
```console
994:   f947e400        ldr     x0, [x0, #4040]
998:   885ffc01        ldaxr   w1, [x0]
99c:   0b020021        add     w1, w1, w2
9a0:   8803fc01        stlxr   w3, w1, [x0]
9a4:   35ffffa3        cbnz    w3, 998 <f+0x5c>
```

Now let’s move to a T4g instance with Graviton2.

**T4g Instance**

Compile the application. This is Neoverse-N1 with LSE. 
 
```console
$ gcc -g atomic.c -o t4g -march=armv8.2-a -lpthread
$ objdump -S t4g > t4g.dis
```

Review the file t4g.dis and check the instructions for incrementing acnt. The sequence is:

- Address of acnt is loaded into x0
- Value of acnt is updated using a single instruction to add 1 to a word in memory

Here is the disassembly:
```console
994:   f947e400        ldr     x0, [x0, #4040]
998:   b8e10002        ldaddal w1, w2, [x0]
```

Staying on the T4g instance, let’s compile with outline-atomics:

```console
$ gcc -g atomic.c -o t4g.outline  -moutline-atomics -lpthread
$ objdump -S t4g.outline > outline.dis
```

Review the file outline.dis and see that the instruction to increment acnt is now a branch to something called __aarch64_ldadd4_acq_rel at address 0xb90:

```console
 a24:   9400005b        bl      b90 <__aarch64_ldadd4_acq_rel>
```

The code for both the load exclusive sequence and the atomic instruction are present. The first section of code is run on the T4g and the second section (after the first ret) is run on the A1. This binary will run on both instances with no changes. In exchange for this flexibility there is the overhead to take a branch and run the correct code path.

```console
0000000000000b90 <__aarch64_ldadd4_acq_rel>:
 b90:   d503245f        bti     c
 b94:   d0000090        adrp    x16, 12000 <__data_start>
 b98:   39404610        ldrb    w16, [x16, #17]
 b9c:   34000070        cbz     w16, ba8 <__aarch64_ldadd4_acq_rel+0x18>
 ba0:   b8e00020        ldaddal w0, w0, [x1]
 ba4:   d65f03c0        ret
 ba8:   2a0003f0        mov     w16, w0
 bac:   885ffc20        ldaxr   w0, [x1]
 bb0:   0b100011        add     w17, w0, w16
 bb4:   880ffc31        stlxr   w15, w17, [x1]
 bb8:   35ffffaf        cbnz    w15, bac <__aarch64_ldadd4_acq_rel+0x1c>
 bbc:   d65f03c0        ret
```

As a final check, move back to the A1 instance and compile for armv8.2-a. The atomic instruction is illegal on the Cortex-A72 and fails.

```console
$ gcc -g atomic.c -o a1 -march=armv8.2-a -lpthread
ubuntu@ip-10-0-0-247:~$ ./a1
Illegal instruction (core dumped)
```

**How can I find out if my application has atomic instructions?**

To check for atomic instructions in applications run objdump on the T4g executable:

```console
$ objdump -d t4g | grep -i 'cas\|casp\|swp\|ldadd\|stadd\|ldclr\|stclr\|ldeor\|steor\|ldset\|stset\|ldsmax\|stsmax\|ldsmin\|stsmin\|ldumax\|stumax\|ldumin\|stumin' | wc -l
```

The above command will report a count of 1 instruction, the ldaddal we looked at. 

To check whether applications contain load exclusives and store exclusives run this command on the A1 executable. It will report a count of 2.

```console
$ objdump -d a1 | grep -i 'ldxr\|ldaxr\|stxr\|stlxr' | wc -l
```

Running on the t4g.outline executable which supports both architectures will report both types of instructions. 

Another way to confirm an executable supports both architectures is to run the command:
```console
$ nm t4g.outline | grep __aarch64_have_lse_atomics | wc -l
```

If it returns a 1 then it was compiled with outline-atomics.

## Summary

Large System Extensions introduce atomic instructions to improve performance for Arm systems with many processors. When migrating applications to Graviton it helps to have an understanding of compilers, compiler options, and libraries. Also, think about the strategy for an application supporting only Graviton2 or also including A1 support. Including A1 support will also enable applications to run on other Arm platforms such as the Raspberry Pi 4. 

Developing applications on AWS Graviton processors is a great way to improve performance and save cost. Let us know what else would help your development projects. 

