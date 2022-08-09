---
title: "IoT Endpoint Software"
Title: "IoT Endpoint Software"
type: docs
description: >
    Learn how find and use IoT Endpoint software and development tools on new projects.
weight: 10
---

{{% pageinfo %}}

IoT endpoints are computing devices that are connected to the edge of the network. They typically collect and serve data by communicating with central or cloud resources. 

Cortex-M and Cortex-A devices are used in IoT endpoints and there are numerous software building blocks which are useful for IoT software developers. 

The information below helps developers learn how to use existing software and development tools in IoT projects.

{{% /pageinfo %}}


## Learn
{{< cardpane >}}
<div class="card text-center">
  <div class="card-header" style="background-color:#95d600;">Introductory</div>
  <div class="card-body">
    <h5 class="card-title"> <b> Get started with Arm Virtual Hardware </b> </h5>
    <p class="card-text">
    <div style="text-align:left">
     <ul >
      <li>Start AVH instance in the cloud</li>
      <li>Build and run an example project</li>
      <li>Remote debug with Arm Development Studio</li>
     </ul>
    </div>
    </p>
    <a href="/iot/avh" class="btn btn-primary">Learn More</a>
  </div>
  <div class="card-footer text-muted">Updated July 12th, 2022</div>
</div>

<div class="card text-center">
  <div class="card-header" style="background-color:#ffc700;">Intermediate</div>
  <div class="card-body">
    <h5 class="card-title"> <b> Get started with Virtual Peripherals </b> </h5>
    <p class="card-text">
    <div style="text-align:left">
     <ul>
      <li>Create a peripheral using Virtual Input/Output (VIO)</li>
      <li>Virtual Streaming Interface (VSI)</li>
      <li>Virtual Socket Interface (VSocket)</li>
   </ul>
   </div>
    </p>
    <a href="/iot/peripherals" class="btn btn-primary">Learn More</a>
  </div>
  <div class="card-footer text-muted">Updated July 13th, 2022</div>
</div>
{{< /cardpane >}}

{{< cardpane >}}
<div class="card text-center">
  <div class="card-header" style="background-color:#95d600;">Introductory</div>
  <div class="card-body">
    <h5 class="card-title"> <b> Get started with Arm Total Solutions for IoT </b> </h5>
    <p class="card-text">
    <div style="text-align:left">
     <ul>
      <li>Get started with ML Evaluation Kit</li>
      <li>Build and run example from Open-IoT-SDK</li>
   </ul>
   </div>
    </p>
    <a href="/iot/total-solutions" class="btn btn-primary">Learn More</a>
  </div>
  <div class="card-footer text-muted">Updated July 13th, 2022</div>
</div>

<div class="card text-center">
  <div class="card-header" style="background-color:#0091bd;">Experienced</div>
  <div class="card-body">
    <h5 class="card-title"> <b> Get started with CI/CD </b> </h5>
    <p class="card-text">
    <div style="text-align:left">
     <ul>
      <li>Prepare a GitHub Repository</li>
      <li>Integrate AVH into a CI/CD flow with GitHub Actions</li>
      <li>Fully automate CI/CD flow with GitHub Actions</li>
      <li>Fully automate CI/CD flow with Jenkins</li>
   </ul>
   </div>
    </p>
    <a href="/iot/cicd" class="btn btn-primary">Learn More</a>
  </div>
  <div class="card-footer text-muted">Updated July 13th, 2022</div>
</div>
{{< /cardpane >}}

{{< cardpane >}}
<div class="card text-center">
  <div class="card-header" style="background-color:#ffc700;">Intermediate</div>
  <div class="card-body">
    <h5 class="card-title"> <b> Run Trusted Firmware-M(TF-M) on Corstone-300 AVH FVP</b> </h5>
    <p class="card-text">
    <div style="text-align:left">
     <ul >
      <li>Build TF-M regression tests</li>
      <li>Run TF-M tests on the Corstone-300 AVH FVP</li>
     </ul>
    </div>
    </p>
    <a href="/iot/tfm" class="btn btn-primary">Learn More</a>
  </div>
  <div class="card-footer text-muted">Updated August 8th, 2022</div>
</div>

<div class="card text-center">
  <div class="card-header" style="background-color:#ffc700;">Intermediate</div>
  <div class="card-body">
    <h5 class="card-title"> <b> Run CMSIS-DSP Tests on Corstone-300 AVH FVP </b> </h5>
    <p class="card-text">
    <div style="text-align:left">
     <ul>
      <li>Build CMSIS-DSP Test framework</li>
      <li>Run CMSIS-DSP tests on Corstone-300 AVH FVP</li>
   </ul>
   </div>
    </p>
    <a href="/iot/cmsis" class="btn btn-primary">Learn More</a>
  </div>
  <div class="card-footer text-muted">Updated August 8th, 2022</div>
</div>
{{< /cardpane >}}


## Reference examples
{{< cardpane >}}
{{< card header="**[Open-IoT-SDK](https://github.com/ARM-software/open-iot-sdk)**" >}}
Arm's Open-IoT-SDK gives you have access to a wide variety of IoT targeted software applications and components ready to run on Arm based platforms. This software framework accelerates intelligent, connected IoT product design by allowing developers to focus on what really matters – innovation and differentiation.
{{< /card >}}

{{< card header="**[Arm ML embedded evaluation kit](https://review.mlplatform.org/plugins/gitiles/ml/ethos-u/ml-embedded-evaluation-kit/)**" >}}
This repository is for building and deploying Machine Learning (ML) applications targeted for Arm® Cortex®-M and Arm® Ethos™-U NPU.
{{< /card >}}
{{< /cardpane >}}

## Other resources

{{< cardpane >}}
{{< card header="**[Arm Virtual Hardware](https://www.arm.com/en/products/development-tools/simulation/virtual-hardware)**" >}}
Arm Virtual Hardware (AVH) delivers test platforms for developers to verify and validate embedded and IoT applications during software design. Multiple modeling technologies are provided that remove the complexity of building and configuring board farms. AVH is useful for continuous integration and continuous development CI/CD (DevOps) and MLOps workflows.
{{< /card >}}

{{< card header="**[Arm Virtual Hardware Lab Series](https://www.arm.com/campaigns/virtual-hardware-lab-series)**" >}}
These recorded virtual sessions include presentation-based sessions and hands-on labs. Developers interested in Arm Virtual Hardware can review the recorded sessions.
{{< /card >}}
{{< /cardpane >}}
