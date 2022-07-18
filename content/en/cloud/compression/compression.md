---
processors: ["Neoverse-N1"]
software: ["linux"]
title: "Measure performance of Compression Libraries on Arm"
linkTitle: "Measure performance of Compression Libraries on Arm"
type: docs
weight: 1
hide_summary: true
description: >
    Learn how to install and benchmark Snappy and Zstandard data compression algorithms on AWS EC2 instances powered by Arm64 achitecture.
---

## Pre-requisites

* Amazon Web Services (AWS) Account 
* AWS EC2 64-bit Arm instance 
* GCC for your Arm Linux distribution. Install using the steps [here](content/en/compilers/install_ngcc)
* Unzip utility 
```console
sudo apt install unzip
```
* Make
```console
sudo apt install make
```

## Detailed Steps

The latest released version of Snappy and Zstandard data compression algorithms are supported on the following Linux distributions:

* Amazon Linux 2
* RHEL/CentOS 8
* Ubuntu Versions - 20.04, 18.04

The detailed steps are provided for an AWS EC2 64-bit Arm instance running Ubuntu.

### Install lzbench

lzbench is an in-memory benchmark of open-source compression algorithms. We will use this benchmark to measure stand-alone performance of the compression algorithms on Arm servers. 

This benchmark also contains the source files for the snappy and zstd compression algorithms among others. They are built as part of the lzbench build process.

On your running EC2 instance, run the following command

```console
git clone https://github.com/inikep/lzbench
make
```

### Install a Dataset to benchmark the compression algorithms

To benchmark the data compression algorithms, you will need a data set to run the compression and decompression algorithms on. In this how-to guide we will use the Silesia corpus data set.

Silesia corpus is a data set of files that covers the typical data types used nowadays. To learn more about this data set and the file contents follow the link [here](https://sun.aei.polsl.pl//~sdeor/index.php?page=silesia)

```console
wget https://sun.aei.polsl.pl//~sdeor/corpus/silesia.zip
unzip silesia.zip
```

### Run lzbench with snappy and zstd

To benchmark the standalone performance of snappy with lzbench, using one of the files(dickens) in the Silesiacorpus data set we installed run the following command

```console
./lzbench -esnappy ../silesia/dickens
```

The value passed to -e in the command above is the compression algorithm

For full usage and viewing all the arguments you can pass to lzbench run the command below

```console
./lzbench
```

To benchmark the standalone performance of zstd with lzbench, using one of the files(dickens) in the Silesiacorpus data set we installed run the following command

```console
./lzbench -ezstd ../silesia/dickens
```

### View Resuls

The Compression, Decompression Throughput and Compression ratio for the files is printed at the end of each of these commands

Below is a table with the results on AWS EC2 Arm 64-bit C6g instance, with Ubuntu 20.04 and gcc 9.3

| File name | Compression Bandwidth (MB/s) | Decompression Bandwidth(MB/s) | Compression Latency (us) | Decompression Latency(us) | Compr Size | Ratio  (%) |
| ---       | ---                          | ---                           | ---                      | ---                       | ---        | ---        |
|snappy	    | ../silesia/nci	           | 755 | 1900	| 44271 | 17684 |	6146795 |	18.32 |
|snappy	    | ../silesia/xml              | 555 | 1462 | 9609  | 3659  |	1308581 |	24.48 |
snappy	../silesia/samba |	471 |	1146 |	45841 |	18907 |	8057361 |	37.29 |
snappy	../silesia/webster |	296 |	729 |	139904 |	56786 |	20211213 |	48.75 |
snappy	../silesia/reymont |	290 |	640 |	22833 |	10352 |	3234968 |	48.81 |
snappy	../silesia/mozilla |	388 |	973 |	131761 |	52582 |	26690826 |	52.11 |
snappy	../silesia/osdb |	457 |	1211 |	22004 |	8340 |	5412825 | 	53.67 |
snappy	../silesia/mr |	373 |	787 |	26649 |	12658 |	5440451 |	54.57 |
snappy	../silesia/dickens |	244 |	548 |	41656 |	18563 |	6340267 |	62.21 |
snappy	../silesia/ooffice |	292 |	820 |	21028 |	7509 |	4311901 | 	70.09 |
snappy	../silesia/sao	313 |	829 |	23175 |	8715 |	6469352 |	89.21 |
snappy	../silesia/x-ray |	6626 |	11654 |	1270 |	698 |	8459794 |	99.83 |
memcpy	../silesia/webster |	15322 |	14941 |	2709 |	2763 |	41458703 |	100 |




