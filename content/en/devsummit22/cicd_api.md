---
title: "Control Arm Virtual Hardware with Javascript/Python/C API"
linkTitle: "CI/CD workflow API"
type: docs
toc_hide: true
hide_summary: true
description: >
    Control Arm Virtual Hardware with Javascript/Python/C API.
---
## Overview

In this section we will learn how to control Arm Virtual Hardware via the [API](https://app.avh.arm.com/api/docs). This can be used stand-alone, or as part of your overall CI/CD workflow. Applications to interface with the API can be written in JavaScript, Python, or C. This example uses JavaScript.

## Pre-requisites

* Arm Virtual Hardware instances managed by GitHub Actions as per [previous section](/devsummit22/cicd_sh).
* Active GitHub account to host repository

## Detailed Instructions

We shall extend the workflow from the previous section to automatically transmit the `chip-tool` commands.

### Set up API Key

In the `Arm Virtual Hardware` browser, navigate to `Profile` > `API`. Generate and copy your `API Key`. This is a unique key that enables remote access to your instance(s).

In the `github` browser, go to your forked repository, and navigate to `Settings` > `Secrets` > `Actions`, and create a `New repository secret`.

Name the secret:
```console
API_TOKEN
```
and paste the above `API Key` as the secret value.

The secret name must be exactly `API_TOKEN`, as this is used by the workflow later.

### Modify workflow

Edit `.github/workflows/cicd_demo.yml` to append this `job` to the workflow:
```yml
  chip_tool:
    needs: rebuild_lighting_app
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Install Node
        uses: actions/setup-node@aa759c6c94d3800c55b8601f21ba4b2371704cb7
        with:
          node-version: 14.17.2

      - name: Install  API
        run: npm install @arm-avh/avh-api --save
      - name: Run script
        env:
          API_TOKEN: ${{ secrets.API_TOKEN }}
        run: node .github/workflows/chip_tool.js
```
This job invokes the following `JavaScript` which will transmit the `on/off` commands to the `chip-tool` instance via the `Websocket` interface.

Create `.github/workflows/chip_tool.js`, with the below:
```js
const readline = require('readline')
const { ArmApi, ApiClient } = require('@arm-avh/avh-api');

const BearerAuth = ApiClient.instance.authentications['BearerAuth']
const api = new ArmApi()

const path = require("path");
const fs = require("fs");

async function main() {
    const apiToken = process.env.API_TOKEN
    
    console.log('Logging in...');
    const authInfo = await api.v1AuthLogin({ apiToken });
    BearerAuth.accessToken = authInfo.token
    
    console.log('Listing projects...');
    let projects = await api.v1GetProjects();
    let project = projects[0];
    
    console.log("Getting Chip Tool instance...");
    let instances = await api.v1GetInstances()
    let instance = instances[0];
    
    console.log("Get Websocket...");
    let url = await api.instance.v1console();
    mySocket = new WebSocket(url);

    console.log("Wait for chip-lighting-app to initialize...");
    await delay(10000);
    
    for(let loop=0; loop<5; loop++>){
        console.log("Turn light on...");
        mySocket.send("./out/debug/chip-tool onoff on 0x11 1");
        
        console.log("Wait 3 seconds...");
        await delay(3000);

        console.log("Turn light off...");
        mySocket.send("./out/debug/chip-tool onoff off 0x11 1");

        console.log("Wait 3 seconds...");
        await delay(3000);
    }
    
    console.log('Run completed');
    return;
}

main().catch((err) => {
    console.error(err);
});
```
**TO DO**
See api.yml in my github
How to use websocket to sent commands to the Chip Tool RP4?
**TO DO**

Push these changes to your repository:
```console
git add .
git commit -m "automate chip-tool"
git push
```
which will trigger a new workflow run.

### Follow progress in GitHub Actions

Navigate to the `Actions` tab of your GitHub repository, and open the current workflow to follow progress. Observe that there are now three `jobs`, with the jobs to run `chip-lighting-app` and `chip-tool` executing in parallel. You can follow progress, and observe `chip-tool` toggling `chip-lighting-app` automatically.

Congratulations! We have entirely automated the process to build and test our applications.

## Next Steps

[Proceed to next section -->](/devsummit22/knowledgecheck)\
[<-- Return to Workshop Home](/devsummit22/#sections)