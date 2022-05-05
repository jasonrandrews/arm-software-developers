---
date: 2021-05-25
title: "Arm-based OCI Ampere A1 Compute instances beat the latest competition on NGINX"
linkTitle: "NGINX on Arm"
description: "Compare performance on NGINX Plus between three Oracle Cloud Infrastructure (OCI)"
author: Steve Demski and Julio Suarez
resources:
- src: "**.{png,jpg}"
---

## Introduction

Oracle Cloud Infrastructure (OCI) has recently launched the Ampere A1 Compute family of Arm Neoverse N1-based VMs and bare-metal instances. These A1 instances use Ampere Altra CPUs that were designed specifically to deliver performance, scalability, and security for cloud applications. The A1 Flex VM family supports an unmatched number of VM shapes that can be configured with 1-80 cores and 1-512GB of RAM (up to 64GB per core). Ampere A1 compute is also offered in bare-metal configurations with up to 2-sockets and 160-cores per instance.

In this blog, we compare the performance and performance per dollar on NGINX Plus between three OCI compute families:

* A1.Flex: Ampere® Altra® CPUs based on Arm Neoverse N1 cores, 3.0GHz all-core sustained max
* E4.Flex: AMD EPYC third generation processors, 2.55GHz base, 3.5GHz single-core turbo
* Optimized3.Flex: latest third Gen Intel Xeon (Ice Lake) scalable processors, 3.0GHz base, 3.6GHz single-core turbo

As of April 30, 2021, as measured by Netcraft1, NGINX remains the most popular scale-out web application server with over 35% market share (powering over 432m web servers). NGINX is available in both open-source and commercially supported NGINX Plus versions. In this blog, we test NGINX Plus in two configurations, as a Reverse Proxy server and as an API Gateway server. For each configuration, we also look at performance with no transaction authorization and with transaction authorization enabled using HS256. As NGNX Plus is typically deployed behind a corporate firewall, these both represent common real-world use case scenarios.

## Pricing Information

The pricing for these Intel, AMD, and Ampere-based instances are listed in Table 1. One notable aspect of the OCI Ampere A1 instance is it the first family to offer $0.01 per-hour per-core pricing. Besides offering a lower price per physical CPU core, Ampere A1 also provides a tiered pricing policy, where the first 3,000 OCPU hours and 18,000GB hours per month are free.


| OCI Virtual Machine | Per OCPU per hour($) | Per GB memory($) | Tiered Pricing |
| ------------------- | -------------------- | ---------------- | -------------- |
| Intel.VM.Optimized3 | 0.054                | 0.0015           | No             |
| AMD.VM.E4           | 0.025                | 0.0015           | No             |
| Ampere.VM.A1        | 0.01                 | 0.0015           | Yes            |


 Table 1: OCI VM pricing information

## System and test configurations

In our evaluation, we measure performance on each instance family by scaling from two hardware threads up to 16 hardware threads, using 8GB of memory per hardware thread. Each instance runs NGINX 1.19.5 (nginx-plus-r23), built using gcc 8.3.1 20190507. The OS is Oracle Linux 8.3 (gcc), built with OpenSSL 1.1.1c FIPS 28-May-2019 (running OpenSSL 1.1.1g FIPS 21-Apr-2020). For both Reverse Proxy and API Gateway testing, we use a common test configuration. For load generation, we use a single E4.Flex instance (32 cores, 64 hardware threads) running the wrk2 benchmark to issue HTTPS requests. And for request responses we use eight instances of E4.Flex (16 cores, 32 hardware threads). The OCI instance under test sits between the load generator and the responding file servers, with requests per second measured between the client and the instance under test.

## Key findings

The Arm Neoverse N1-based OCI Ampere A1 Compute instance family delivers superior performance per dollar over both the Xeon-based Optimized3 (Intel Xeon Ice Lake) instances and over the EPYC-based E4 instances. This is true for both Reverse Proxy and API Gateway testing configurations. And it is true with both no transaction authorization ("No Auth") and for HS256 transaction authorization turned on. Compared to Xeon-based Ice Lake instances the OCI Ampere A1 instances provide up to 69% better performance per dollar. And compared to EPYC-based E4 instances the OCI Ampere A1 instances provide up to 62% better performance per dollar.

{{< imgproc nginx_blog_1 Fill "600x300" >}}
Figure 1: NGINX Plus reverse proxy (no authorization) server request per second per dollar comparison between OCI A1 (Altra), E4 (EPYC) and Optimized3 (Xeon Ice Lake) instance families.
{{< /imgproc >}}

We believe requests per second per dollar is the figure of merit for which most customers will choose to optimize. But the pure performance and scalability of these Altra-based A1 instances is still very strong.

Figure 2 shows the Reverse Proxy, no authorization, requests per second between the three instance families. For each hardware thread size, the A1 (Altra) instance is able to outperform the E4 (EPYC) instance by up to 46%. The Optimized3 (Xeon) instance family shows good performance at lower hardware thread count but scales performance poorly compared to the Ampere A1 family. At 16 hardware threads the A1 performance is within 5% of the Optimized3 performance.

{{< imgproc nginx_blog_2 Fill "600x300" >}}
Figure 2: NGINX Plus reverse proxy (no authorization) server request per second comparison between OCI A1 (Altra), E4 (EPYC) and Optimized3 (Xeon) instance families.
{{< /imgproc >}}

For brevity, we will not show every combination of testing configuration here, but the results of NGNX Plus as a proxy server with HS256 authorization, and as an API Gateway (no auth, and with HS256) closely mirror the results we see previously for NGINX Plus proxy server with no authorization. You can see this in figures 3, 4, and 5.

One key observation, regardless of tested configuration, is that the Ampere A1 Compute family achieves maximum performance and performance per dollar with 16 hardware threads. This, we believe, is a result of the Ampere Altra CPU making using of both the Arm Neoverse N1 core and the Arm Neoverse CMN-600 mesh interconnect. Each of these IPs was designed to deliver performance and scalability on server workloads and that result is what we are seeing here.  

{{< imgproc nginx_blog_3 Fill "600x300" >}}
Figure 3: NGINX Plus API gateway (no authorization) server request per second per dollar comparison between OCI A1 (Altra), E4 (EPYC) and Optimized3 (Xeon) instance families.
{{< /imgproc >}}

{{< imgproc nginx_blog_4 Fill "600x300" >}}
Figure 4: NGINX Plus reverse proxy (HS256 authorization) server request per second per dollar comparison between OCI A1 (Altra), E4 (EPYC) and Optimized3 (Xeon) instance families.
{{< /imgproc >}}

{{< imgproc nginx_blog_5 Fill "600x300" >}}
Figure 5: NGINX Plus API gateway (HS256 authorization) server request per second per dollar comparison between OCI A1 (Altra), E4 (EPYC) and Optimized3 (Xeon) instance families.
{{< /imgproc >}}

## Conclusion

Organizations of every size are under constant pressure to reduce costs while maintaining (or improving) their service level responsiveness. This is true of all services but web services (Reverse Proxy and API Gateway) are particularly common and it is noticeable when issues occur. With their family of Arm Neoverse N1-based Ampere A1 Compute instances, Oracle Cloud Infrastructure is setting out to deliver great performance and performance scalability while minimizing price per transaction. With up to 69% higher performance per dollar on NGNX Plus over competitive offerings Arm-based Ampere A1 delivers amazing performance and value. And we believe similar performance, scalability and performance per dollar results are achievable on Ampere A1 instances across a broad range of cloud and enterprise workloads. Oracle is also making it easy to get started out testing this Ampere A1 family with the introduction of their "always free" tier. With this Free Tier offering, customers can try out up to 4 A1 cores and 24GB of memory absolutely free. For more information on this family of OCI Ampere A1 instances, please visit the Oracle Ampere A1 product website.

[Learn more about OCI A1 instances](https://www.arm.com/partners/oracle)

## Resources

1. Netcraft April 2021 web server [survey](https://news.netcraft.com/archives/category/web-server-survey/)

2. Oracle pricing information: https://www.oracle.com/cloud/compute/pricing.html

