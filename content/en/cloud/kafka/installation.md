---
processors : ["Neoverse-N1"]
software : ["linux"]
title: "Install Zookeeper & Kafka"
type: docs
weight: 2
hide_summary: true
description: >
    Learn how to install Java, Zookeeper, and Kafka.
---

## Prerequisites

* 7 Physical machines or 7 cloud nodes with Ubuntu/Debian installed. We need 3 Kafka nodes, 3 Zookeeper nodes, and 1 client node.

**Note**: we can download latest Kafka binary from [here](https://dlcdn.apache.org/kafka/).

## Install Java:

We need to run Java install commands on all 7 nodes.

```console

apt install -y default-jdk

```

## Install Zookeeper(3.8.0):

Zookeeper needs to be install on the 3 Zookeeper nodes as shown below.

```console

mkdir Zookeeper

wget https://dlcdn.apache.org/zookeeper/zookeeper-3.8.0/apache-zookeeper-3.8.0-bin.tar.gz

tar -xzf apache-zookeeper-3.8.0-bin.tar.gz

cd apache-zookeeper-3.8.0-bin

```

Create a Zookeeper directory on each node.

```console

mkdir  /tmp/zookeeper

echo 1 >> /tmp/zookeeper/myid

```

## Install Kafka:

Kafka needs to be install on the 3 Kafka nodes as shown below.

```console

mkdir Kafka

wget https://dlcdn.apache.org/kafka/3.2.3/kafka_2.13-3.2.3.tgz

tar -xzf kafka_2.13-3.2.3.tgz

cd kafka_2.13-3.2.3

```
Create a Kafka log directory on each node.

```console

mkdir /tmp/kafka-logs

```

[<-- Return to Learning Path](/content/en/cloud/kafka/#sections)
