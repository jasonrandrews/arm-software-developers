---
title: "Prepare GitHub repository for CI/CD development"
linkTitle: "Prepare GitHub repository"
type: docs
description: >
    Learn how to prepare a repository for a CI/CD development flow with Arm Virtual Hardware.
---
## Overview
in this section you will learn how to prepare a GitHub repository for a CI/CD development flow.

Full instructions are given in the Arm Virtual Hardware [documentation](https://arm-software.github.io/AVH/main/examples/html/GetStarted.html)

## Pre-requisites

* A valid [GitHub](https://github.com) account
* [An Arm Virtual Hardware instance running in the cloud](/iot/aws/launch)

## Detailed steps

### Fork or copy the example repository

As we shall be making modifications to the reference example, you must make your own copy (`fork`) of the repository.\
In a web browser, navigate to the repository at:
```console
https://github.com/ARM-software/AVH-TFLmicrospeech/fork
```
and create a copy in your own personal repository store (you must be logged into GitHub).\
It is assumed below that you have used the same repository name (`AVH-TFLmicrospeech`) for your fork.

### Personal Access Token

GitHub requires that a [Personal Access Token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token) be set. If you do not have this on your account already, navigate to `Settings` > `Developer Settings` > `Personal Access Tokens`, click on `Generate new token`, and save the token locally.

### Clone this repository

In your Arm Virtual Hardware terminal, clone the FORK of the repository, and navigate into its directory.
```console
git clone https://github.com/<GitHub_Username>/AVH-TFLmicrospeech
cd AVH-TFLmicrospeech/Platform_FVP_Corstone_SSE-300_Ethos-U55
```
### Build the example

Rebuild the project:
```console
cbuild.sh microspeech.Example.cprj
```
The build will take some time to complete.

### Run the example

Run the example on `Arm Virtual Hardware for Corstone-300`.
```console
 ./run_example.sh
 ```
 Observe the output.
 ```
Heard yes (146) @1000ms
Heard no (145) @5600ms
Heard yes (143) @9100ms
Heard no (145) @13600ms
...
```
### Change the example

Edit `command_responder.cc` source file, which defines the output message.
```console
nano ../micro_speech/src/command_responder.cc
```
For example, change `Heard` to `The word was` in the `TF_LITE_REPORT_ERROR()` function.

### Rebuild and rerun

Rebuild and rerun the example.
```console
cbuild.sh microspeech.Example.cprj
./run_example.sh
```
Observe that the output has changed as expected.
```
The word was yes (146) @1000ms
The word was no (145) @5600ms
The word was yes (143) @9100ms
The word was no (145) @13600ms
...
```
### Update the GitHub repository

Set your GitHub login details in your Virtual Hardware instance
```console
git config --global user.name "<GitHub_Username>"
git config --global user.email <Email>
```
Verify that the fork of the repository is referenced
```console
git remote -v
```
Commit and push changed file(s) to the repository
```
git add ../micro_speech/src/command_responder.cc
git commit -m "changed output message"
git push
```
You will be prompted for your GitHub username and Personal Access Token.

Refresh your browser and observe that your fork of the repository has been updated appropriately.
## Next Steps

Learn how to [configure GitHub Actions to automatically run tests](/iot/cicd/gh-mspeech)
