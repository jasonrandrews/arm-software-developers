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

GitHub now requires a [Personal Access Token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token) when pushing remote updates.

If you do not know your token, you can create a new one via `Settings` > `Developer Settings` > `Personal access tokens`.

Ensure you have enabled the token to `Update GitHub Action workflows`.

## Detailed Instructions

In the `lighting-app` console, stop the app (`Ctrl+C`) if still running.

### Prepare repository for workshop

The Matter repository from where the examples are sourced contains very many workflows for rebuilding different configurations. For the convenience of time, let us remove these, and install only our new workflow.

In the `lighting-app` console, navigate to the `.github/workflows` folder, and delete all.
```console
cd /home/pi/connectedhomeip/.github/workflows
rm -rf *.yaml
rm -rf *.yml
```
Create a `.yml` textfile, for example with the `nano` editor:
```console
nano cicd_demo.yml
```
Copy the below to that file. If you have issues copying and pasting all of this in one go, you may need to paste in smaller sections.
```yml
name: Matter_CICD_Demo

on:
  push:
    branches: [ master ]
  workflow_dispatch:

jobs:
  rebuild_lighting_app:
    runs-on: self-hosted
    steps:
     - uses: actions/checkout@v2
     
     - name: submodules
       run: ./scripts/checkout_submodules.py --shallow --platform linux
       
     - name: bootstrap and build
       run: |
         ./scripts/build/gn_bootstrap.sh
         source scripts/activate.sh
         cd examples/lighting-app/linux
         gn gen out/debug
         ninja -C out/debug
         
  run_lighting_app:
    needs: rebuild_lighting_app
    runs-on: self-hosted
    steps:
      - name: Run lighting-app for 1 minute
        run: |
          cd examples/lighting-app/linux
          timeout 120s ./out/debug/chip-lighting-app || code=$?; if [[ $code -ne 124 && $code -ne 0 ]]; then exit $code; fi
```
When done, exit `nano` (`Crtl+X`), and enter `Y`(yes) when prompted to save buffer and use same filename.

For the purposes of time, we shall `push` these changes later.

### Create GitHub self-hosted runner

Browse to the forked Matter repository in your personal GitHub space.

Navigate to `Settings` > `Actions` > `Runners`, and then click on `New self-hosted runner`.

Configure for `Linux` host on `ARM64` Architecture (the `host` of the runner will be the `lighting-app` Virtual Raspberry Pi 4 instance).

You will see a set of commands (unique to you) to download and configure the `runner`.

In the `lighting-app` console, return to your home directory:
```console
cd /home/pi
```
Copy and paste the `Download` and `Configure` commands (from GitHub) for your `self-hosted runner`.\
It is OK to select the default options when prompted during configuration.

To keep the console available for later use, run the `self-hosted runner agent` as a background service:
```console
sudo ./svc.sh install pi
sudo ./svc.sh start
sudo ./svc.sh status
```
In your GitHub repository, you will see your runner listed (`Settings` > `Actions` > `Runners`), with `Idle` status.

### Make a code change

In the `lighting-app` console, make a code change, for example, editing the output message when light is toggled.

This is in a source file named `on-off-server.cpp`. Open the file with `nano`.
```console 
cd /home/pi/connectedhomeip
nano src/app/clusters/on-off-server/on-off-server.cpp
```
Locate the `Toggle on/off` message (use `Ctrl+_` to jump to line `137`):
```C
    emberAfOnOffClusterPrintln("Toggle on/off from %x to %x", currentValue, newValue);
```
Edit to give a new output message, for example:
```C
    emberAfOnOffClusterPrintln("HELLO WORLD! Toggle on/off from %x to %x", currentValue, newValue);
```
Exit (`Ctrl+X`) and save your change.

### Push changes to GitHub repository and invoke workflow

The `yml` code contains the below, which tells GitHub to invoke this workflow whenever there is a `push` to the repository.
```yml
on:
  push:
    branches: [ master ]
```
To push the changes, in `lighting-app` console, first enter your GitHub credentials.
```console
git config --global user.name "YOUR_GITHUB_USERNAME"
git config --global user.email YOUR_EMAIL_ADDRESS
```
Ensure you are pushing these changes to your personal forked repository.
```console
git remote -v 
```
Commit the changes to your repository.
```console
git add .
git commit -m "delete other workflows, update output message"
git push
```
You will be prompted for your GitHub username and `Personal Access Token` (password).

The workflow contains two `jobs`, which rebuild, and then run `lighting-app`:
```yml
jobs:
  rebuild_lighting_app:
...
  run_lighting_app:
```
Note that `rebuild_lighting_app` will take a few minutes to complete, as it must repeat all the initialization steps for the Matter build system.

### Follow the workflow progress in GitHub Actions

The workflow does not output on the target, but rather logs to GitHub. You can follow the workflow steps, and see the output logs in your GitHub repository, under the `Actions` tab.

After `lighting-app` is initialized, you can toggle the light with your `chip-tool` instance as before:
```console
./out/debug/chip-tool onoff on 0x11 1
./out/debug/chip-tool onoff off 0x11 1
```
Observer your new message in the `run_lighting_app` log, for example:
```
[TIMESTAMP][INSTANCEID] CHIP:ZCL: HELLO WORLD! Toggle on/off from 1 to 0
```
The workflow will cleanly terminate `lighting-app` after 120 seconds.

## Next Steps

[Proceed to next section -->](/devsummit22/cicd_api)\
[<-- Return to Workshop Home](/devsummit22/#sections)