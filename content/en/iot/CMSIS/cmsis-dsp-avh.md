---
processors: [Cortex-M55]
software: [bare-metal]
title: "Run CMSIS-DSP Tests on Corstone-300 AVH FVP"
linkTitle: ""
type: docs
weight: 1
hide_summary: true
description: >
   Follow the instructions in this guide to build and run CMSIS-DSP tests on Corstone-300 FVP included in AVH.
---

## Learning Objectives 

By the end of this guide, you will be able to:

* Build CMSIS-DSP tests for the Corstone-300 AVH FVP 
* Run CMSIS-DSP tests on the Corstone-300 AVH FVP

## Pre-requisites

* AWS Account
* AWS EC2 instance running AVH AMI. Use the instructions [here](iot/avh/launch)

## Detailed Steps

### Build the CMSIS-DSP tests

On the launched EC2 instance running the AVH AMI, install python 3 pre-requisites for CMSIS-DSP

```console
sudo apt update
sudo ln -s /usr/local/bin/pip3 /usr/bin/pip3.8
pip install --upgrade pip
pip install pyparsing
pip install Colorama
```

Next, clone the CMSIS-DSP git repository and switch to the latest working branch with the commits applicable to AVH

```console
git clone https://github.com/ARM-software/CMSIS-DSP/
git checkout -b a973e9e
```

Now, build the test framework and generate all the C files needed using the steps below

```console
cd CMSIS-DSP/Testing
createDefaultFolder.sh
python preprocess.py -f desc.txt
python preprocess.py -f desc_f16.txt -o Output_f16.pickle
python processTests.py -e
python processTests.py -e -f Output_f16.pickle
```

Select the test suite you would like to build the tests for. For example, run the command below to build all the BasicTests for F32 data type

```console
python processTests.py -e BasicTestsF32
```

CMSIS-DSP repository has a cmsis_build directory with all the files to build the tests for different AVH simulation targets. Run the commands below to first install the CMSIS-DSP pack and then build the selected tests for Corstone-300 AVH FVP  .

```console
cd cmsis_build
cpackget pack add https://github.com/ARM-software/CMSIS-DSP/releases/download/v1.11.0/ARM.CMSIS-DSP.1.11.0.pack
cbuild.sh "test.Release+VHT-Corstone-300.cprj"  --outdir=Objects --intdir=Tmp
```
The output executables from the build are created in the Objects directory as specified by the command.

### Run the CMSIS-DSP tests on the Corstone-300 FVP

Now that we have successfully built the CMSIS-DSP suite of tests, we are ready it to run it on the Corstone-300 FVP that is already installed on the AMI.

Use the command below to launch the simulation with the CMSIS-DSP tests

```console
VHT_Corstone_SSE-300_Ethos-U55 -a Objects/test.Release+VHT-Corstone-300.axf -f configs/ARM_VHT_Corstone_300_config.txt > results.txt
````

You will see some raw output like the one shown below. This output needs be post-processed to understand the results.

```
S: g 1
S: g 1
S: g 6
S: s 2
S: t
S: 1 0 0 0 Y
E:
b
S: t
S: 2 0 0 0 Y
E:
b
S: t
S: 3 0 0 0 Y
E:
b
S: t
S: 4 0 0 0 Y
E:
b
S: t
S: 5 0 0 0 Y
E:
b
S: t
S: 6 0 0 0 Y
E:
b
S: t
S: 7 0 0 0 Y
E:
b
S: t
S: 8 0 0 0 Y
E:
b
S: t
S: 9 0 0 0 Y
E:
b
S: t
S: 10 0 0 0 Y
E:
b
S: t
S: 11 0 0 0 Y
```

To post-process the raw output and view the results, run the command below

```console
python ../processResult.py -f ../Output.pickle -e -r results.txt
```

Now, you will see the test pass/fail status for each of the CMSIS-DSPs tests that you run

```
The cycles displayed by this script must not be trusted.
They are just an indication. The timing code has not yet been validated.

Group : Root  (1)
  Group : DSP Tests  (1)
    Group : Basic Tests  (6)
      Suite : Basic Tests F32 (2)
        Test nb=3    arm_add_f32 (test_add_f32 - 1) : PASSED
        Test nb=4n   arm_add_f32 (test_add_f32 - 2) : PASSED
        Test nb=4n+1 arm_add_f32 (test_add_f32 - 3) : PASSED
        Test nb=3    arm_sub_f32 (test_sub_f32 - 4) : PASSED
        Test nb=4n   arm_sub_f32 (test_sub_f32 - 5) : PASSED
        Test nb=4n+1 arm_sub_f32 (test_sub_f32 - 6) : PASSED
        Test nb=3    arm_mult_f32 (test_mult_f32 - 7) : PASSED
        Test nb=4n   arm_mult_f32 (test_mult_f32 - 8) : PASSED
        Test nb=4n+1 arm_mult_f32 (test_mult_f32 - 9) : PASSED
        Test nb=3    arm_negate_f32 (test_negate_f32 - 10) : PASSED
        Test nb=4n   arm_negate_f32 (test_negate_f32 - 11) : PASSED
        Test nb=4n+1 arm_negate_f32 (test_negate_f32 - 12) : PASSED
        Test nb=3    arm_offset_f32 (test_offset_f32 - 13) : PASSED
        Test nb=4n   arm_offset_f32 (test_offset_f32 - 14) : PASSED
        Test nb=4n+1 arm_offset_f32 (test_offset_f32 - 15) : PASSED
        Test nb=3    arm_scale_f32 (test_scale_f32 - 16) : PASSED
        Test nb=4n   arm_scale_f32 (test_scale_f32 - 17) : PASSED
        Test nb=4n+1 arm_scale_f32 (test_scale_f32 - 18) : PASSED
        Test nb=3    arm_dot_prod_f32 (test_dot_prod_f32 - 19) : PASSED
        Test nb=4n   arm_dot_prod_f32 (test_dot_prod_f32 - 20) : PASSED
        Test nb=4n+1 arm_dot_prod_f32 (test_dot_prod_f32 - 21) : PASSED
        Test nb=3    arm_abs_f32 (test_abs_f32 - 22) : PASSED
        Test nb=4n   arm_abs_f32 (test_abs_f32 - 23) : PASSED
        Test nb=4n+1 arm_abs_f32 (test_abs_f32 - 24) : PASSED
        Test long    arm_add_f32 (test_add_f32 - 25) : PASSED
        Test long    arm_sub_f32 (test_sub_f32 - 26) : PASSED
        Test long    arm_mult_f32 (test_mult_f32 - 27) : PASSED
        Test long    arm_negate_f32 (test_negate_f32 - 28) : PASSED
        Test long    arm_offset_f32 (test_offset_f32 - 29) : PASSED
        Test long    arm_scale_f32 (test_scale_f32 - 30) : PASSED
        Test long    arm_dot_prod_f32 (test_dot_prod_f32 - 31) : PASSED
        Test long    arm_abs_f32 (test_abs_f32 - 32) : PASSED
        Test 1       arm_clip_f32 (test_clip_f32 - 33) : PASSED
        Test 2       arm_clip_f32 (test_clip_f32 - 34) : PASSED
        Test 3       arm_clip_f32 (test_clip_f32 - 35) : PASSED
```




