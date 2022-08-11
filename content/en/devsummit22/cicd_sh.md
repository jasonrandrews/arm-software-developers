---
title: "Manage development in a CI/CD workflow with Self-Hosted Runner"
linkTitle: "CI/CD workflow self-hosted runner"
type: docs
toc_hide: true
hide_summary: true
description: >
    Manage development in a CI/CD workflow using GitHub Actions.
---
## Overview

In this section we will learn how to manage ongoing development in an automated CI/CD workflow, using [GitHub Actions](https://github.com/features/actions) and self-hosted runner.

## Pre-requisites

* Arm Virtual Hardware instance with Matter applications built as per [previous section](/devsummit22/build).
* Active GitHub account to host repository

GitHub requires a [Personal Access Token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token) to push updates.\
If you do not know your token, you can create a new one via `Settings` > `Developer Settings` > `Personal access tokens`.

## Detailed Instructions

In the `lighting-app` console, stop the app (`Ctrl+C`) if still running.

### Prepare repository for workshop

The Matter repository from where the examples are sourced contains very many workflows for rebuilding different configurations.\
For the convenience of time, let us remove these, and install only our workflow.

In the `lighting-app` console, navigate to the `workflows` folder, and delete all.
```console
cd /home/pi/connectedhomeip/.github/workflows
rm -rf *.yaml
rm -rf *.yml
```
Create a textfile `cicd_demo.yml` (the name is arbitrary, but .yml is necessary), containing the below
```console

WILL COPY WHEN ALL FINISHED
See  https://github.com/RonanSynnottArm/connectedhomeip/.github/workflows

```
To push these changes, you will likely need to supply your GitHub credentials.
```console
git config --global user.name "YOUR_GITHUB_USERNAME"
git config --global user.email your.email@address.com
```
Ensure you are pushing these changes to your personal forked repository.
```console
git remote -v 
```
Commit the changes to your repository.
```console
git add .
git commit -m "delete other workflows"
git push
```
You will be prompted for your GitHub login and `Personal Access Token`.

### Create GitHub self-hosted runner

Browse to the forked Matter repository in your personal GitHub space.\
Navigate to `Settings` > `Actions` > `Runners`, and then click on `New self-hosted runner`.\
Configure for `Linux` host on `ARM64` Architecture (this is the configuration of the Virtual Raspberry Pi 4 instance).\
You will see a set of commands (unique to you) to download and configure the `runner` on the (`lighting-app`) Raspberry Pi 4 instance.

In the `lighting-app` console, return to your home directory:
```console
cd /home/pi
```
Copy and paste the download and configure commands for the `runner`.\
It is OK to select the default options when prompted during configuration.

After configuration, to keep the `CONSOLE` free, log into the Raspberry Pi 4 via the CLCD screen, and launch the runner from there:
```console
cd actions-runner
./run.sh
```
When launched, you should see a message similar to:
```
TIMESTAMP: Listening for Jobs
```
### Make a code change

Return to the `lighting-app/linux` folder:
```console 
cd /home/pi/connectedhomeip/examples/lighting-app/linux
```
We will change the output message when light is toggled. This is set in `on-off-server.cpp`.\
Using a text editor, such as `nano`:
```console
nano ../../../src/app/clusters/on-off-server/on-off-server.cpp
```
Locate the `Toggle on/off` message (circa line 137), and edit to give a new output message, for example:
```C
    emberAfOnOffClusterPrintln("HELLO WORLD Toggle on/off from %x to %x", currentValue, newValue);
```
Rebuild:
```console
gn gen out/debug
ninja -C out/debug
```
and re-run application:
```console
./out/debug/chip-lighting-app
```
When `chip-lighting-app` is initialized, toggle the light with your `chip-tool` instance:
```console
./out/debug/chip-tool onoff on 0x11 1
./out/debug/chip-tool onoff off 0x11 1
```
Observer your new message in the `chip-lighting-app` log:
```
[TIMESTAMP][INSTANCEID] CHIP:ZCL: HELLO WORLD Toggle on/off from 1 to 0
```
When satisfied, kill `chip-lighting-app` with `Ctrl+C`.

### To do

Almost working... see workflows in my github
https://github.com/RonanSynnottArm/connectedhomeip/.github/workflows


## Next Steps
[Proceed to next section -->](/devsummit22/cicd_api)
[<-- Return to Workshop Home](/devsummit22/#sections)