---
processors: ["Cortex-M"]
softwares: ["bare-metal"]
tools: ["RTL-simulator"]

title: "Collect Code Coverage from RTL simulation"
linkTitle: "Collect Code Coverage from RTL simulation"
type: docs
toc_hide: true
hide_summary: true
description: >
    This is a tutorial about collecting code coverage.
---

Arm DesignStart provides access to popular Arm IP to start a custom SoC Design or to explore and learn about custom SoC development. The Cortex-M0 and Cortex-M3 are currently available for instant access. There are numerous technical resources to learn about the Armv6-M and Armv7-M architectures and the AMBA 3 AHB protocol. DesignStart is also a wonderful way to learn about logic simulation and embedded software development.

One of the fun things about DesignStart is that anybody can learn and experiment with real hardware simulation and software development. EDA partners such as Cadence and Mentor are even offering access to tools which can be used with DesignStart. The DesignStart blog contains a number of articles and the forum has many helpful questions and answers.

For a practical example of how to ensure embedded software is fully exercised and tested, let’s create rudimentary instruction coverage and source line coverage for software running on the Cortex-M3 DesignStart eval package. Code coverage is a valuable tool to identify code which is untested or could be removed.

## Getting started

To get started download the Cortex-M3 DesignStart eval package. Just click the “Access” button for Cortex-M3 to get started. This requires an Arm account but can be done with a click through license for instant access. Rather than repeat all of the setup instructions, I recommend watching the video showing how to simulate the hello world application. The DesignStart eval package offers two options to simulate the Cortex-M3. One is obfuscated RTL and the other is a Cycle Model. Obfuscated RTL is Verilog source code which is a little hard to read but compiles and simulates as Verilog source code. The Cycle Model is compiled Verilog RTL with a SystemC wrapper which can be used in any simulator which supports mixing Verilog and SystemC. The video explains the differences between the Cortex-M3 obfuscated RTL and the Cycle Model, but one of the primary benefits of the Cycle Model is generation of a tarmac trace file showing executed instructions and memory accesses. The code coverage flow depends on the tarmac trace file so the Cycle Model is required for this exercise.

The tarmac trace file can be used for creating code coverage information. All Arm CPUs generate tarmac trace files so this is a great skill to learn as it applies to every Arm SoC design project.

After downloading the Cortex-M3 DesignStart eval package you will get an e-mail that contains a link to get a free, one-year Cycle Model license. Make sure to get the license and install it. When simulating always select the Cycle Model to enable generation of the tarmac trace file.

Once the .tgz file is downloaded let’s do a quick review of how to setup a simulation.

```console
$ mkdir cm3ds ; cd cm3ds
$ tar xvfz ~/Downloads/AT421-MN-80001-r0p0-02rel0.tgz
$ cd AT421-MN-80001-r0p0-02rel0
```

The most relevant documentation file for simulation is in the docs/ directory. I recommend keeping docs/arm_cortex_m3_designstart_eval_rtl_and_testbench_user_guide_100894_0000_00_en.pdf open to find information about the simulation options.

## Running simulations
Navigate to the testbench directory and compile the design:

```console
$ cd m3designstart/logical/testbench/execution_tb
```

The options to select the simulator can be passed on the command line or set in the make.cfg file.

I like to edit the make.cfg file so I can forget about some of the options on the command line, but either way works fine. I set SIMULATOR=ius, SIM_VCD=yes, and DSM=yes to specify to use the Cycle Model.

DesignStart eval supports Cadence, Mentor, and Synopsys simulators. I’m using the Cadence simulator, but to use one of the other simulators simply set the SIMULATOR value and refer to the pdf file for more information.


```console
#-----------------------------------------------------------------------------
# The confidential and proprietary information contained in this file may
# only be used by a person authorised under and to the extent permitted
# by a subsisting licensing agreement from ARM Limited.
#
#            (C) COPYRIGHT 2013-2017 ARM Limited.
#                ALL RIGHTS RESERVED
#
# This entire notice must be reproduced on all copies of this file
# and copies of this file may only be made by a person if such person is
# permitted to do so under the terms of a subsisting license agreement
# from ARM Limited.
#
#      SVN Information
#
#      Checked In          : $Date: 2013-02-08 16:27:43 +0000 (Fri, 08 Feb 2013) $
#
#      Revision            : $Revision: 236695 $
#
#      Release Information : CM3DesignStart-r0p0-02rel0
#
#-----------------------------------------------------------------------------
# Purpose:
#
#   This file contains options that configure aspects of the execution
#   testbench.  You can edit this file to change these options.
#-------------------------------------------------------------------------------
# Testbench options. Set an option to yes to enable, no to disable.
DSM            := yes   # Set to 'yes' to use the carbon model with register visibility and tarmac
                        # TARMAC config is ignored unless DSM is set to 'yes'
TARMAC         := yes   # Enable tarmac trace of code as it is executed
SIM_64BIT      := yes   # Use 64-bit simulation
SIM_VCD        := yes   # Turn off VCD output
GUI            := no    # Non interactive simulation
FSDB           := no    # Disable FSDB output

MAX_SIMULATION_TIME := 40000us # Default maximum simulation time

# Compilation options
TOOL_CHAIN     := ds5  # Default C compiler is gcc

# Simulator
SIMULATOR      := ius  # Default simulator is Mentor ModelSim

# PlusArgs
#PLUSARGS        +=

# BuildOpts
#BUILDOPTS       +=

# Source code paths
TESTCODES_PATH    = ../testcodes

# Important notes:
# ================
#
#  1. If you change any of the testbench options in this file you must run
#     'make clean' on the top-level Makefile and then recompile the testbench.
#
#  2. 64-bit simulation is only possible on 64-bit operating systems
```

After editing make.cfg compile the design:

```console
$ make compile
 >> Compiling testbench with ius   and DSM=yes   
(irun -f tbench_cm.vc +define+IUS_BUILD -elaborate -nospecify +access+r -scautoshell systemc -sysc /home/jasand01/cm3ds/AT421-MN-80001-r0p0-02rel0/m3designstart/logical/testbench/execution_tb/../../../../cortexm3_model/libcortexm3_integrationds_dsm.a -D__x86_64__ /home/jasand01/cm3ds/AT421-MN-80001-r0p0-02rel0/m3designstart/logical/testbench/execution_tb/../../../../cortexm3_model/CORTEXM3INTEGRATIONDS_dsm.cpp -I/home/jasand01/cm3ds/AT421-MN-80001-r0p0-02rel0/m3designstart/logical/testbench/execution_tb/../../../../cortexm3_model -L/home/jasand01/cm3ds/AT421-MN-80001-r0p0-02rel0/m3designstart/logical/testbench/execution_tb/../../../../cortexm3_model -lcarbon5 +define+ARM_CM +define+ARM_DSM +define+VCD_ON -64bit ) > ius_compile.log
 >> Testbench compile with ius   and DSM=yes     completed successfully, log in ius_compile.log
 ```

Next, run a simulation and generate a tarmac file

```console
$ make run TESTNAME=hello
 >> Running testbench with ius   and DSM=yes   
export LD_LIBRARY_PATH=:/home/jasand01/cm3ds/AT421-MN-80001-r0p0-02rel0/m3designstart/logical/testbench/execution_tb/../../../../cortexm3_model:/arm/tools/arm/socd/9.5.0/deps/gcc/current_version/lib64:/arm/tools/arm/cms/9.4.0/Linux64/gcc472/lib64:/arm/tools/arm/cms/9.4.0/Linux64/lib/gcc/shared:/arm/tools/arm/cms/9.4.0/Linux64/lib:/lib:/usr/lib:/arm/tools/platform/lsf/10.1_nahpc/linux3.10-glibc2.17-x86_64/lib; export TARMAC_ENABLE=1; irun  -R -unbuffered -64bit -input run.tcl < quit.do | tee "ius_hello_run.log"
irun(64): 15.20-s005: (c) Copyright 1995-2016 Cadence Design Systems, Inc.
Loading snapshot worklib.tb_fpga_shield:v .................... Done
CORTEXM3INTEGRATIONDS_dsm.utarmac.utarmacDSM.utarmacI: -----------------------------------------------
CORTEXM3INTEGRATIONDS_dsm.utarmac.utarmacDSM.utarmacI: ARM/Thumb UAL Verilog Disassembler
CORTEXM3INTEGRATIONDS_dsm.utarmac.utarmacDSM.utarmacI: (c) ARM Limited 2006-2009 - All Rights Reserved
CORTEXM3INTEGRATIONDS_dsm.utarmac.utarmacDSM.utarmacI: -----------------------------------------------
ncsim> source /arm/tools/cadence/incisive/15.20.005/tools/inca/files/ncsimrc
ncsim> run 40000us 
Loading CXDT from parameter IMAGENAME (./CXDT.bin)
*
* Max. address:                        001ffff
* Begin of full protection address:    0000000
* Begin of half protection address:    0010000
* Begin of quarter protection address: 0018000
*
===========================================================

 nvSRAM Power UP 
*
* Max. address:                        001ffff
* Begin of full protection address:    0000000
* Begin of half protection address:    0010000
* Begin of quarter protection address: 0018000
*
===========================================================

 nvSRAM Power UP 
*
* Max. address:                        001ffff
* Begin of full protection address:    0000000
* Begin of half protection address:    0010000
* Begin of quarter protection address: 0018000
*
===========================================================

 nvSRAM Power UP 

===========================================================

tarmac: Generating trace file cm_tarmac.log using handle 00000002

===========================================================
130040.000ns UART: Hello world 
161640.000ns UART: ** TEST PASSED ** 
164720.000ns UART: Test Ended
Simulation stopped via $stop(1) at time 164720 NS + 1
../verilog/cmsdk_uart_capture_ard.v:240       $stop;
```

This will generate a cm_tarmac.log file which contains the instructions executed, registers changed, and the memory accessed. The file tarmac.txt, also in the execution_tb/ directory, explains how to interpret the tarmac trace file format. This is an appropriate time to watch the video about RTL debugging to learn more about how to understand the simulation.

## Software examples

There are numerous software examples included with the DesignStart package and most are more interesting than the hello world program. Let’s use the interrupt_demo test to calculate code coverage. The main source file is m3designstart/software/common/demos/interrupt_demo.c

An ELF image for the software is needed to map the instructions to the source code, but only the .bin file is provided in the DesignStart package with the option of recompiling the software using either gcc, DS-5, or Keil MDK. The compiler is not important for the code coverage calculations as any of them will work, but with logic simulation on Linux I selected DS-5, which uses Arm Compiler 5 (armcc) in the makefile. To build the interrupt_demo with Arm Compiler 5 make sure DS-5 is installed. Trial licenses are available on the downloads page.

To setup armcc and compile use:

```console
$ /usr/local/DS-5_v5.29.1/bin/suite_exec -t "Arm Compiler 5 (DS-5 built-in)"  bash
$ cd ~/cm3ds/AT421-MN-80001-r0p0-02rel0/m3designstart/logical/testbench/testcodes/interrupt_demo
$ make TOOL_CHAIN=ds5
```

This will create a new .bin file and leave behind interrupt_demo.ELF which can be used to generate code coverage.

Run the interrupt demo:

```console
$ make run TESTNAME=interrupt_demo
irun(64): 15.20-s005: (c) Copyright 1995-2016 Cadence Design Systems, Inc.
Loading snapshot worklib.tb_fpga_shield:v .................... Done
CORTEXM3INTEGRATIONDS_dsm.utarmac.utarmacDSM.utarmacI: -----------------------------------------------
CORTEXM3INTEGRATIONDS_dsm.utarmac.utarmacDSM.utarmacI: ARM/Thumb UAL Verilog Disassembler
CORTEXM3INTEGRATIONDS_dsm.utarmac.utarmacDSM.utarmacI: (c) ARM Limited 2006-2009 - All Rights Reserved
CORTEXM3INTEGRATIONDS_dsm.utarmac.utarmacDSM.utarmacI: -----------------------------------------------
ncsim> source /arm/tools/cadence/incisive/15.20.005/tools/inca/files/ncsimrc
ncsim> run 40000us
Loading CXDT from parameter IMAGENAME (./CXDT.bin)
*
* Max. address:                        001ffff
* Begin of full protection address:    0000000
* Begin of half protection address:    0010000
* Begin of quarter protection address: 0018000
*
===========================================================

 nvSRAM Power UP
*
* Max. address:                        001ffff
* Begin of full protection address:    0000000
* Begin of half protection address:    0010000
* Begin of quarter protection address: 0018000
*
===========================================================

 nvSRAM Power UP
*
* Max. address:                        001ffff
* Begin of full protection address:    0000000
* Begin of half protection address:    0010000
* Begin of quarter protection address: 0018000
*
===========================================================

 nvSRAM Power UP

===========================================================

tarmac: Generating trace file cm_tarmac.log using handle 00000002

===========================================================
112080.000ns UART:
182080.000ns UART: Cortex-M3 DesignStart - Interrupt Demo - revision $Revision: 243249 $
183240.000ns UART:
185440.000ns UART:
186440.000ns UART:
187440.000ns UART:
188600.000ns UART:
217160.000ns UART: +*************************+
245720.000ns UART: *                         *
274280.000ns UART: *  Timer0 Interrupt demo  *
302840.000ns UART: *                         *
331240.000ns UART: +*************************+
332240.000ns UART:
333400.000ns UART:
363960.000ns UART:    [Timer 0 IRQ]
384080.000ns UART:    Timer test done
386760.000ns UART:
387760.000ns UART:
388760.000ns UART:
389920.000ns UART:
418480.000ns UART: +*************************+
447040.000ns UART: *                         *
475600.000ns UART: *  GPIO PORT0: Interrupt  *
504160.000ns UART: *         Example         *
532720.000ns UART: *                         *
561120.000ns UART: +*************************+
562120.000ns UART:
563280.000ns UART:
593600.000ns UART:     ...Test GPIO0[7]...
594760.000ns UART:
617520.000ns UART:       High Level IRQ:
640520.000ns UART:      Detected On Pin 7
641520.000ns UART:
642680.000ns UART:
669800.000ns UART:     ...Test GPIO0[8]...
670960.000ns UART:
692600.000ns UART:        Low Level IRQ
715600.000ns UART:      Detected On Pin 8
716600.000ns UART:
717760.000ns UART:
744800.000ns UART:     ...Test GPIO0[9]...
745960.000ns UART:
768600.000ns UART:       Rising Edge IRQ
791600.000ns UART:      Detected On Pin 9
792600.000ns UART:
793760.000ns UART:
821800.000ns UART:     ...Test GPIO0[10]...
822960.000ns UART:
846600.000ns UART:      Falling Edge IRQ:
870600.000ns UART:      Detected On Pin 10
871600.000ns UART:
872760.000ns UART:
927520.000ns UART:     All 4 IRQs Detected
929400.000ns UART:
933640.000ns UART:
934800.000ns UART:
962360.000ns UART:  +***********************+
989920.000ns UART:  *                       *
1017480.000ns UART:  *   GPIO 0 IRQ Tests    *
1045040.000ns UART:  *  Passed Successfully  *
1072600.000ns UART:  *                       *
1100000.000ns UART:  +***********************+
1101160.000ns UART:
1132600.000ns UART: +*************************+
1161160.000ns UART: *                         *
1189720.000ns UART: *   UART Interrupt demo   *
1218280.000ns UART: *                         *
1246680.000ns UART: +*************************+
1247680.000ns UART:
1248840.000ns UART:
1315880.000ns UART: Transmit message : hello world
3607720.000ns UART: Received message : hello world
3626120.000ns UART:
3628000.000ns UART:
3667280.000ns UART: IRQNUM: 32          PASS
3669160.000ns UART:
3691400.000ns UART: ** TEST PASSED **
3692560.000ns UART:
3693200.000ns UART: Test Ended
Simulation stopped via $stop(1) at time 3693200 NS + 1
../verilog/cmsdk_uart_capture_ard.v:240       $stop;
ncsim>
```

This generates a new cm_tarmac.log file for the version of interrupt_demo compiled with Arm Compiler 5.

Simple instruction and source line coverage can be calculated using the cm_tarmac.log and the interrupt_demo.ELF.

A python script is attached to the bottom of this article which reads the tarmac file and generates the coverage. Make sure cc-tarmac.py has execute permission and print the usage message:

```console
$ ./cc-tarmac.py -h
usage: cc-tarmac.py [-h] [-t TARMACFILE] [-e ELFFILE] [-c COMPILER]
                    [-g GNUPREFIX] [-l LLVMTRIPLE] [-o OUTFILE] [-d]

optional arguments:
  -h, --help            show this help message and exit
  -t TARMACFILE, --tarmac-file TARMACFILE
                        existing tarmac file from RTL simulation
  -e ELFFILE, --elf-file ELFFILE
                        input software image, preferably with debugging
                        information
  -c COMPILER, --compiler COMPILER
                        compiler used: arm, gnu, llvm
  -g GNUPREFIX, --gnu-prefix GNUPREFIX
                        gnu prefix to add to the front of objdump
  -l LLVMTRIPLE, --llvm-triple LLVMTRIPLE
                        string to pass to llvm-objdump via -triple
  -o OUTFILE, --output OUTFILE
                        coverage output file
  -d, --debug           turn on debug print statements
  ```

The primary script inputs are the tarmac trace file and the ELF file for the software. If the Arm compiler is selected the fromelf utility is also used to generate the disassembly file for coverage annotation so make sure the selected compiler is setup in the terminal where the script is run. Similar utilities are used for the gcc and llvm compilers.

To generate the code coverage use:

```console
$ ./cc-tarmac.py  -t cm_tarmac.log -e ../testcodes/interrupt_demo/interrupt_demo.ELF  -c arm
Using tarmac file cm_tarmac.log
Using elf file ../testcodes/interrupt_demo/interrupt_demo.ELF
Using out file ../testcodes/interrupt_demo/interrupt_demo.ELF.cov
reading tarmac file ...
tarmac shows 66863 instructions executed
868 instructions are unique


868 instructions covered
665 instructions NOT covered
56.6% instruction coverage

207 source lines covered
265 source lines NOT covered
43.9% source line coverage
```

In addition to the statistics printed there are two new files generated, one for instruction coverage and one for source line coverage. The instruction coverage is the disassembly of the software with a count in front of each instruction showing how many times the instruction was executed. For the interrupt_demo the created file name is interrupt_demo.ELF.cov_arm_asm.

The source code line coverage is generated in the file interrupt_demo.ELF.cov_arm_src. It contains the path to the source file with the line number and column number of the code. The beginning of each line shows how many times that line of source code was executed. This can be used to find unexecuted code and may reveal surprises about how often particular line of code was executed.

Both files are generated in the directory containing the .ELF file so make sure to look there and not in the directory where the simulation was run. I have attached the contents of both files at the bottom of the article along with the script to create them.

This simple technique is just one of the many ways to create code coverage for Cortex-M software. Keil MDK has built in code coverage with ULINKpro and multiple Arm partners provide code coverage using instrumented software or real-time trace, but the technique described here is useful for non-intrusive, pre-silicon logic simulation.

## Summary

DesignStart makes it easy to access real Cortex-M designs to start a custom SoC design project or to learn about simulation and software development. Software debugging can be done with a waveform and tarmac trace file and it’s easy to create additional scripts to help analyze results and identify problems. Future DesignStart topics include learning how to create embedded software which can be built with multiple compilers to increase code quality and provide choices for performance and code size. Using Arm Fast Models to develop embedded software is another way to more efficiently debug new software compared to running it on a Verilog simulator and using the tarmac trace and waveform.
 
Please contact me directly on the Arm Community if you would like to run the cc-tarmac.py script. It relies on two other Python pacakges, tarmac and pyelftools, which may require additional information, especially if you don’t have sudo or root access on the simulation machine. I enjoy building scripts and tools that help with debug and analysis of Arm simulation and always interested to hear from others who are doing similar things.
