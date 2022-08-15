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
Create a textfile `cicd_demo.yml` containing the below:
```yml
# example workflow to manage Arm Virtual Hardware with Self-Hosted Runner
name: AVH_RPi4_Matter

# When the workflow will run
on:
  workflow_dispatch:
  push:
    branches: [ main ]
#  pull_request:
#    branches: [ main ]

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
          timeout 60s ./out/debug/chip-lighting-app || code=$?; if [[ $code -ne 124 && $code -ne 0 ]]; then exit $code; fi
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
You will be prompted for your GitHub username and `Personal Access Token` (password).

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

After configuration, to keep the `CONSOLE` free, log into the Raspberry Pi 4 via the CLCD screen interface, and launch the runner from there:\
Username: `pi`\
Password: `raspberry`
```console
cd actions-runner
./run.sh
```
When launched, you should see a message similar to:
```
TIMESTAMP: Listening for Jobs
```
### Make a code change

In the `lighting-app` console, make a code change, editing the output message when light is toggled. This is set in a source file named `on-off-server.cpp`.
```console 
cd /home/pi/connectedhomeip
nano src/app/clusters/on-off-server/on-off-server.cpp
```
Locate the `Toggle on/off` message (circa line 137):
```C
    emberAfOnOffClusterPrintln("Toggle on/off from %x to %x", currentValue, newValue);
```
Edit to give a new output message, for example:
```C
    emberAfOnOffClusterPrintln("HELLO WORLD! Toggle on/off from %x to %x", currentValue, newValue);
```
Exit (`Ctrl+X`) and save your change.

### Push change to GitHub and invoke workflow

The `yml` code contains the below, which tells GitHub to invoke this workflow whenever there is a `push` to the repository. This means that any update will automatically trigger a new test of the code.
```yml
on:
  push:
    branches: [ main ]
```
In the `lighting-app` console, push the code change to GitHub:
```console
git add .
git commit -m "Toggle output message changed"
git push
```
The workflow contains two `jobs`, which rebuild, and then run `chip-lighting-app`:
```yml
jobs:
  rebuild_lighting_app:
...
  run_lighting_app:
```
You can follow this in the `runner`, which will output messages such as:
```
TIMESTAMP: Running job rebuild_lighting_app
```
Note that `rebuild_lighting_app` will take a few minutes to complete, as it must repeat all the initialization steps for the Matter build system.

### Follow the workflow progress in GitHub Actions

The workflow does not output on the target, but rather logs to GitHub. You can follow the workflow steps, and see the output logs in your GitHub repository, under the `Actions` tab.

When `chip-lighting-app` is initialized, toggle the light with your `chip-tool` instance:
```console
./out/debug/chip-tool onoff on 0x11 1
./out/debug/chip-tool onoff off 0x11 1
```
Observer your new message in the `run_lighting_app` log:
```
[TIMESTAMP][INSTANCEID] CHIP:ZCL: HELLO WORLD! Toggle on/off from 1 to 0
```
The workflow will automatically terminate `chip-lighting-app` after 60 seconds.

## Next Steps

[Proceed to next section -->](/devsummit22/cicd_api)\
[<-- Return to Workshop Home](/devsummit22/#sections)