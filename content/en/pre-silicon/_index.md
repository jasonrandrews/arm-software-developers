
---
title: "Pre-Silicon Development" 
type: docs
weight: 2
description: >
    General information and how-to articles to accelerate Pre-Silicon development for Arm devices. 
---

{{% pageinfo %}}
This section provides important information for software engineers working on Arm SoC design projects.

The learning path modules listed below are applicable if you are a software engineers creating code that interacts directly with hardware.

Common tasks include:
* Develop boot code
* Create hardware diagnostic tests
* Write bare metal software
* Benchmark software performance

{{% /pageinfo %}}

{{< cardpane >}}

<div class="card text-center">
  <div class="card-header" style="background-color:#95d600;">Introductory</div>
  <div class="card-body">
    <h5 class="card-title"> <b> Develop bare-metal software for Arm devices without hardware </b> </h5>
    <p class="card-text">
    <div style="text-align:left">
     <ul >
      <li>Understand boot code and linker files</li>
      <li>Build your first application running on an Arm virtual platform</li>
      <li>Modify the same application to use different I/O mechanisms</li>
     </ul>
    </div>
    </p>
    <a href="/pre-silicon/bare-metal-lp" class="btn btn-primary">Learn More</a>
  </div>
  <div class="card-footer text-muted">Updated June 27th, 2022</div>
</div>

<div class="card text-center">
  <div class="card-header" style="background-color:#ffc700;">Intermediate</div>
  <div class="card-body">
    <h5 class="card-title"> <b> Benchmark Cortex-M software </b> </h5>
    <p class="card-text">
    <div style="text-align:left">
     <ul>
      <li>High level benchmarking with Systick Timer</li>
      <li>CPU level benchmarking with DWT counters</li>
      <li>Detailed benchmarking with PMU events</li>
   </ul>
   </div>
    </p>
    <a href="/pre-silicon/bm_cortexm" class="btn btn-primary">Learn More</a>
  </div>
  <div class="card-footer text-muted">Updated August 16th, 2022</div>
</div>

{{< /cardpane >}}
