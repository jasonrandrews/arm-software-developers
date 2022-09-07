---
processors: ["Neoverse-N1"]
software: ["linux"]
title: "Run memcached on Arm servers and measure performance"
linkTitle: "Run memcached on Arm servers and measure performance"
type: docs
weight: 1
hide_summary: true
description: >
    Learn how to install and run memcached on AWS EC2 instances powered by Arm64 achitecture.
---

## Pre-requisites

* Amazon Web Services (AWS) Account 
* AWS EC2 64-bit Arm instance running Ubuntu 20.04
* Install gcc on the running EC2 instance following the steps [here]()
* Install libevent
```console
sudo apt install libevent-dev -y
```
* Install the packages required by memtier_benchmark
```console
sudo apt install build-essential autoconf automake libpcre3-dev libevent-dev pkg-config zlib1g-dev libssl-dev -y
```

## Detailed Steps

The latest released version of MongoDB Community Edition (5.0) is supported on the following Linux distributions:

* Amazon Linux 2
* RHEL/CentOS 8
* Ubuntu Versions - 20.04, 18.04

Refer to this [page](https://www.mongodb.com/docs/manual/administration/production-notes/#platform-support-matrix) for the complete platform support matrix 

### Install memcached from source on Arm servers

Using your AWS Account, launch an Arm 64-bit EC2 instance running Ubuntu 20.04.

Then run through the steps below to install memcached on your EC2 instance.

```console
wget http://memcached.org/files/memcached-1.6.17.tar.gz
tar -zxvf memcached-1.6.17.tar.gz
cd memcached-1.6.17
./configure && make && make test && sudo make install
```

### Run memcached on Arm server

Now run the following command to run memcached

```console
/usr/local/bin/memcached
```

### Install memtier_benchmark

memtier_benchmark is a command line utility developed by Redis Labs for load generation and bechmarking NoSQL key-value databases. We will use this to benchmark the performance of memcached running on your 64-bit Arm AWS EC2 instance

```console
git clone https://github.com/RedisLabs/memtier_benchmark
cd memtier_benchmark
autoreconf -ivf
./configure
make
sudo make install
```

### Measure memcached performance by running memtier_benchmark

Use the following command to run memtier_benchmark and measure the performance of memcached

```console
memtier_benchmark -s localhost -p 11211 --protocol=memcache_text --clients=100 --threads=5 --ratio=1:1 --key-pattern=R:R --key-minimum=16 --key-maximum=16 --data-size=128 --requests=10000 --run-count=20
```

To understand what each of the command line options do, run the following command

```console
memtier_benchmark --help
```

### View Results

At the end of the benchmark run, the aggrerated performance results are printed on the console. For example, using the command above the output is as follows

```
AGGREGATED AVERAGE RESULTS (20 runs)
============================================================================================================================
Type         Ops/sec     Hits/sec   Misses/sec    Avg. Latency     p50 Latency     p99 Latency   p99.9 Latency       KB/sec
----------------------------------------------------------------------------------------------------------------------------
Sets       187514.94          ---          ---         1.33816         1.12700         2.84700         7.42300     29665.45
Gets       187514.94    187514.94         0.00         1.33374         1.12700         2.83100         7.39100     32046.01
Waits           0.00          ---          ---             ---             ---             ---             ---          ---
Totals     375029.89    187514.94         0.00         1.33595         1.12700         2.84700         7.42300     61711.46
```


[<-- Return to Learning Path](/cloud/memcached/#sections)



