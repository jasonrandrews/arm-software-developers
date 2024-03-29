---
title: "AVH Workshop at DevSummit 2022"
linkTitle: "AVH Workshop at DevSummit 2022"
type: docs
hide_summary: true
weight: 4
description: >-
     Instructions for attendees of the Arm Virtual Hardware workshop at DevSummit 2022
---
## Overview

Welcome to Arm DevSummit 2022. This workshop is to show you how to get started developing with [Matter](https://buildwithmatter.com) and [Arm Virtual Hardware](https://www.arm.com/products/development-tools/simulation/virtual-hardware).

**Attendees must provide their own laptop (recommended) or tablet.**

This session is a hands-on workshop connecting to Arm Virtual Hardware in the cloud. Arm Virtual Hardware has been thoroughly tested with Chrome, Firefox, and Safari browsers.

## Learning Objectives

By the end of this workshop, you will be able to:
* Instantiate Arm Virtual Hardware instances
* Build and run Matter examples on Arm Virtual Hardware
  * Demonstrate communication between two virtual hardware targets
* Use [GitHub Actions](https://github.com/features/actions) to manage ongoing development
  * Automated CI/CD workflow

## Prerequisites

To participate in the workshops, users must prepare **in advance** of the workshop:

 - User account for [Arm Virtual Hardware](https://avh.arm.com/)
 - User account for [GitHub](https://github.com/)

GitHub now requires a [Personal Access Token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token) when pushing remote updates.

If you do not know your token, you can create a new one via `Settings` > `Developer Settings` > `Personal access tokens`.

Ensure you have enabled the token to `Update GitHub Action workflows`.

You may wish to create a local scratchpad text file containing the below details (which will be unique to you), so that you can easily copy-and-paste from. These will be used frequently during this workshop.
```
YOUR_GITHUB_USERNAME
YOUR_PERSONAL_ACCESS_TOKEN
git config --global user.name "YOUR_GITHUB_USERNAME"
git config --global user.email YOUR_EMAIL_ADDRESS
```

## Sections

|          Type   | Content       |
| ---             | ---           |
| How-To          | [Setup Arm Virtual Hardware (Raspberry Pi 4)](/devsummit22/setup) |
| How-To          | [Build and run Matter examples on Arm Virtual Hardware](/devsummit22/build) |
| How-To          | [Automate CI/CD workflow with Self-Hosted Runner](/devsummit22/cicd_sh) |
| How-To          | [Control Virtual Hardware with API](/devsummit22/cicd_api) |
| Optional How-To | [Connect to instance via SSH](/devsummit22/ssh) |
| Check           | [Knowledge check and review](/devsummit22/knowledgecheck) |

## References and Documentation

| Type          | Content             |
| ---           | ---                 |
| Reference     | [Arm Virtual Hardware](https://avh.arm.com)      |
| Documentation | [AVH Product Overview](https://arm-software.github.io/AVH/main/overview/html/index.html) |
| Documentation | [Building Matter](https://github.com/project-chip/connectedhomeip/blob/master/docs/guides/BUILDING.md) |

## Next Steps

See the rest of the Arm DevSummit 2022 [program](https://devsummit.arm.com).

Learn about [Arm in IoT](https://www.arm.com/solutions/iot).
