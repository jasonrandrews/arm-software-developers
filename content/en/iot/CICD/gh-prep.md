---
title: "Prepare GitHub repository for CI/CD development"
linkTitle: "Prepare GitHub repository"
type: docs
description: >
    Learn how to prepare a repository for a CI/CD development flow with Arm Virtual Hardware.
---
## Overview
in this section you will learn how to prepare a GitHub repository for a CI/CD development flow. An [example project](https://github.com/ARM-software/AVH-GetStarted) is provided to enable you to quickly get started.

Full instructions are given in the Arm Virtual Hardware [documentation](https://arm-software.github.io/AVH/main/examples/html/GetStarted.html)

## Pre-requisites

* A valid [GitHub](https://github.com) account
* [An Arm Virtual Hardware instance running in the cloud](/iot/aws/launch)

## Detailed steps

### Fork or copy the example repository

As we shall be making modifications to the reference example, you must make your own copy of the repository. In a web browser, navigate to the repository at:
```console
https://github.com/ARM-software/AVH-GetStarted
```
Click either `Use this template` or `Fork` to create a copy in your own personal repository store. It is assumed below that you have used the same repository name (`AVH-GetStarted`) for your copy.

### Personal Access Token

GitHub requires that a [Personal Access Token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token) be set. If you do not have this on your account, navigate to `Settings` > `Developer Settings` > `Personal Access Tokens`, and click on `Generate new token`.


### Clone this repository

In your Arm Virtual Hardware terminal, clone the COPY of the repository, and navigate into its directory.
```console
git clone https://github.com/<YourGitHubName>/AVH-GetStarted
cd AVH-GetStarted
```
### Build the basic example

In your Arm Virtual Hardware terminal, navigate into the `basic` directory, and build the example.
```console
cd basic
cbuild.sh basic.debug.cprj
```
### Run the example

Run the example on `Arm Virtual Hardware for Corstone-300`.
```console
 VHT_Corstone_SSE-300_Ethos-U55 -a Objects/basic.axf -f vht_config.txt
 ```
 Observe in the output that one of the tests failed.
 ```
---[ UNITY BEGIN ]---
/home/ubuntu/AVH-GetStarted/basic/main.c:57:test_my_sum_pos:PASS
/home/ubuntu/AVH-GetStarted/basic/main.c:58:test_my_sum_neg:PASS
/home/ubuntu/AVH-GetStarted/basic/main.c:48:test_my_sum_fail:FAIL: Expected 2 Was 0
/home/ubuntu/AVH-GetStarted/basic/main.c:60:test_my_sum_zero:PASS
-----------------------
4 Tests 1 Failures 0 Ignored
FAIL
---[ UNITY END ]---
```
### Fix the example

Edit `main.c` to fix the failing test. For example, change the `TEST_ASSERT_EQUAL_INT` value from `2` to `0`.
```C
/* Failing test with incorrect summation value */
static void test_my_sum_fail(void) {
  const int sum = my_sum(1, -1);
  TEST_ASSERT_EQUAL_INT(0, sum);
}
```
### Rebuild and rerun

Rebuid and rerun the example.
```console
cbuild.sh basic.debug.cprj
VHT_Corstone_SSE-300_Ethos-U55 -a Objects/basic.axf -f vht_config.txt
```
Observe in the output that all tests passed.
```
---[ UNITY BEGIN ]---
/home/ubuntu/AVH-GetStarted/basic/main.c:57:test_my_sum_pos:PASS
/home/ubuntu/AVH-GetStarted/basic/main.c:58:test_my_sum_neg:PASS
/home/ubuntu/AVH-GetStarted/basic/main.c:59:test_my_sum_fail:PASS
/home/ubuntu/AVH-GetStarted/basic/main.c:60:test_my_sum_zero:PASS
-----------------------
4 Tests 0 Failures 0 Ignored
OK
---[ UNITY END ]---
```
### Update the GitHub repository

Set your GitHub login details in your Virtual Hardware instance
```console
git config --global user.name "<Username>"
git config --global user.email <Email>
```
Verify that the COPY of the repository is referenced
```console
git remote -v
```
Commit and push changed file(s) to the repository
```
git add .
git commit -m "fixed test 3"
git push
```
You will be prompted for your GitHub username and Personal Access Token.

Refresh your browser and observe that your copy of the repository has been updated appropriately.
## Next Steps

Learn how to [configure GitHub Actions to automatically run tests](/iot/cicd/gh-actions)
