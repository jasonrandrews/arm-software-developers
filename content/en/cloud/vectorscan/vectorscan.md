---
processors: ["Neoverse-N1"]
software: ["linux"]
title: "Build Vectorscan on Arm"
linkTitle: "Build Vectorscan on Arm"
type: docs
weight: 1
hide_summary: true
description: >
    Learn how to build Vectorscan, a regex parsing library based on Intel's Hyperscan library on AWS EC2 instances powered by Arm64 achitecture.
---

## Pre-requisites

* Amazon Web Services (AWS) Account 
* AWS EC2 64-bit Arm instance running one of the below Linux ditributions that Vectorscan is known to work on. 
   * RHEL/CentOS 8
   * Ubuntu Versions - 22.04, 20.04, 18.04

The instructions provided below have been tested on an Ubuntu 22.04 AWS 64-bit Arm EC2 instance (C6g.xlarge) 

* GCC for your Arm Linux distribution. Install using the steps [here](content/en/compilers/install_ngcc)
* cmake - used here as the build system
```console
sudo apt install cmake
```
* Boost
```console
sudo apt install libboost-all-dev
```
* Ragel
```console
sudo apt install ragel
```
* PkgConfig
```console
sudo apt install pkg-config
```
* Sqlite3
```console
sudo apt install libsqlite3-dev
```
* libpcap - Package for capturing network packets
```console
sudo apt install libpcap-dev
```

## Detailed Steps

[Vectorscan](https://github.com/VectorCamp/vectorscan) is an architecture-inclusive fork of [Hyperscan](https://github.com/intel/hyperscan), that preserves the support for x86 and modifies the framework to allow for Arm architectures and vector engine implementations.

The detailed steps are provided for an AWS EC2 64-bit Arm instance running Ubuntu 22.04.

### Install Vectorscan

Start by cloning the git repository for Vectorscan.

```console
git clone https://github.com/VectorCamp/vectorscan.git
cd vectoscan
```

### Edit environment variables and fix PCRE download location

First fix the PCRE download location in the cmake file. Open cmake/setenv-arm64-cross.sh in an editor of your choice.

```console
vi cmake/setenv-arm64-cross.sh
```
Change `wget -O pcre-8.41.tar.bz2 https://ftp.pcre.org/pub/pcre/pcre-8.41.tar.bz2` to `wget -O pcre-8.41.tar.bz2 https://sourceforge.net/projects/pcre/files/pcre/8.41/pcre-8.41.tar.bz2/download`

In the same file, now set the environment variables to match the location of your GCC compiler, Boost libraries and PCRE installation. The snippet below is an example with the default installation locations.
```console
export BOOST_VERSION=1_57_0
export BOOST_DOT_VERSION=${BOOST_VERSION//_/.}
export CROSS=/usr/bin/aarch64-linux-gnu-
export CROSS_SYS=/

# if [ ! -d "boost_$BOOST_VERSION" ];
# then
#       wget -O boost_$BOOST_VERSION.tar.gz https://sourceforge.net/projects/boost/files/boost/$BOOST_DOT_VERSION/boost_$BOOST_VERSION.tar.gz/download
#       tar xf boost_$BOOST_VERSION.tar.gz
# fi
if [ ! -d "pcre-8.41" ];
then
        wget -O pcre-8.41.tar.bz2 https://sourceforge.net/projects/pcre/files/pcre/8.41/pcre-8.41.tar.bz2/download
        tar xf pcre-8.41.tar.bz2
        export PCRE_SOURCE=./pcre-8.41
fi

export BOOST_PATH=/usr/include
```

Now source this file

```console
source cmake/setenv-arm64-cross.sh
```

### Fix source to build with glibc>=2.34

There is a current issue where builds fail with glibc >=2.34 and a pending [PR](https://github.com/intel/hyperscan/issues/359)

For now workaround this issue by making the changes to STACK_SIZE mentioned in the pull request.

### Configure Vectorscan with cmake

Create build directory and configure cmake to build vectorscan. 

```console
mkdir vectorscan-build
cd vectorscan-build
cmake -DCROSS_COMPILE_AARCH64=1 ../ -DCMAKE_TOOLCHAIN_FILE=../cmake/arm64-cross.cmake
```

To build vectorscan on targets with Scalable Vector Enginer (SVE) support, add one of the variables below to your cmake command. Only one of these variables needs to be set as weaker variables will be implied as set.

* BUILD_SVE
* BUILD_SVE2
* BUILD_SVE2_BITPERM

For example

```console 
cmake -DCROSS_COMPILE_AARCH64=1 ../ -DCMAKE_TOOLCHAIN_FILE=../cmake/arm64-cross.cmake -DBUILD_SVE
```

### Build Vectorscan 

In the final step run make to build the vectorscan library

```console
make -jT
```

Where T points to the number of threads used to build

The executables from the build are created in the bin/ directory.

### Run Vectorscan Unit Tests

Run a sanity check to validate Vectorscan is built and running correctly

```console
./bin/unit-vectorscan
```

All the unit tests should run successfully. At the end of execution you will output that looks like this

```
[----------] Global test environment tear-down
[==========] 3746 tests from 33 test cases ran. (197558 ms total)
[  PASSED  ] 3746 tests.
```





































































