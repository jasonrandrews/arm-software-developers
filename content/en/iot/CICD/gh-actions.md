---
title: "Integrate Arm Virtual Hardware into CI/CD with GitHub Actions"
linkTitle: "GitHub Actions"
type: docs
description: >
    Learn how to integrate Arm Virtual Hardware into an automated CI/CD development flow with GitHub Actions.
---
## Overview
in this section you will learn how to inteegrate Arm Virtual Hardware into a CI/CD development flow, and automate with GitHub Actions.

Full instructions are given in the Arm Virtual Hardware [documentation](https://arm-software.github.io/AVH/main/examples/html/GetStarted.html)

## Pre-requisites

* [An Arm Virtual Hardware instance running in the cloud](/iot/aws/launch)
* [An appropriately configured GitHub repository](/iot/cicd/gh-prep)

## Detailed steps

### Enable GitHub Actions

Open your browser, and navigate to your COPY of the repository [set up previously](/iot/cicd/gh-prep). Navigate to `Actions`. If prompted that `workflows` have been disabled, click the `I understand my workflows, go ahead and enable them` button.

### Create a Self-hosted Runner

Navigate to the repository `Settings` > `Actions` > `Runners`, and click on `New self-hosted runner`. Set `Runner image` as `Linux`, and `Architecture` as `x64`. A set of commands will be displayed to run on the Arm Virtual Hardware instance to prepare the runner. These commands will be unique for your account and repository.

Create a second [Virtual Hardware terminal](/iot/avh/launch), and copy and paste these commands to there, and launch the runner. Whem complete it will report that it is `Listening for Jobs`.

### Modify the example sources

Return to the original terminal, and modify `main.c`, setting the `TEST_ASSERT_EQUAL_INT` to a failing value. For example:
```C
/* Failing test with incorrect summation value */
static void test_my_sum_fail(void) {
  const int sum = my_sum(1, -1);
  TEST_ASSERT_EQUAL_INT(20, sum);
}
```
### Rebuild and rerun

Rebuid and rerun the example.
```console
cbuild.sh basic.debug.cprj
VHT_Corstone_SSE-300_Ethos-U55 -a Objects/basic.axf -f vht_config.txt
```
Observe in the output that the test is (correctly) failing.
```
---[ UNITY BEGIN ]---
/home/ubuntu/AVH-GetStarted/basic/main.c:57:test_my_sum_pos:PASS
/home/ubuntu/AVH-GetStarted/basic/main.c:58:test_my_sum_neg:PASS
/home/ubuntu/AVH-GetStarted/basic/main.c:48:test_my_sum_fail:FAIL: Expected 20 Was 0
/home/ubuntu/AVH-GetStarted/basic/main.c:60:test_my_sum_zero:PASS
-----------------------
4 Tests 1 Failures 0 Ignored
FAIL
---[ UNITY END ]---
```

### Update the GitHub repository

Commit and push changed file(s) to the repository
```
git add .
git commit -m "broke test 3"
git push
```
You will be prompted for your GitHub username and Personal Access Token.

Refresh your browser and observe that your copy of the repository has been updated appropriately.

## Runner

TO DO - BASIC EXAMPLE DOES NOT HAVE SELF-HOSTED RUNNER!!!!



## Next Steps

to do

https://github.com/ARM-software/Tool-Solutions/tree/master/mlops-cloud