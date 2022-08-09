---
title: "Fully automate CI/CD development flow with GitHub Actions"
linkTitle: "Fully automate CI/CD"
type: docs
hide_summary: true
description: >
    Learn how to fully automate a CI/CD development flow with GitHub Actions and AWS.
---
## Overview
in this section you will learn how to fully automate your CI/CD development flow, using GitHub Actions workflows to launch Arm Virtual Hardware instances.

Full instructions are given in the Arm Virtual Hardware [documentation](https://arm-software.github.io/AVH/main/examples/html/GetStarted.html).

## Pre-requisites

* Valid AWS and GitHub accounts
* [An understanding of how to use GitHub Actions](/iot/cicd/gh-mspeech)

## Detailed steps

### Fork the example GitHub repository

In a web browser, navigate to the repository at:
```console
https://github.com/ARM-software/AVH-GetStarted/fork
```
and create a fork in your own personal repository store.

In your fork, navigate to `Actions`. If prompted that `workflows` have been disabled, click the `I understand my workflows, go ahead and enable them` button.

### Configure repository for automation TO DO?

To enable GitHub Actions to automate the workflow, you need to define a number of [GitHub Secrets](https://docs.github.com/en/actions/security-guides/encrypted-secrets) with your AWS credentials. These are described in the `basic.yml` file in the `.github/workflows` directory.

Full decription of the steps necessary for this set-up are given [here](https://arm-software.github.io/AVH/main/examples/html/GetStarted.html#GS_SetupCI).

### Run the workflow

Navigate to `Actions`, and select the `basic example`.\
Click `Run workflow` to manually start the workflow.\
Click on the workflow to follow progress.

Observer the output in the `Run tests` step of the `ci_test` job, which reports a failure.
```
/home/ubuntu/AVH-GetStarted/basic/main.c:57:test_my_sum_pos:PASS
/home/ubuntu/AVH-GetStarted/basic/main.c:58:test_my_sum_neg:PASS
/home/ubuntu/AVH-GetStarted/basic/main.c:48:test_my_sum_fail:FAIL: Expected 2 Was 0
/home/ubuntu/AVH-GetStarted/basic/main.c:60:test_my_sum_zero:PASS
```
### Modify the example source

Modify `main.c` in `basic` folder, setting `TEST_ASSERT_EQUAL_INT` argument to `0`, so that it will not fail.
```C
/* Failing test with incorrect summation value */
static void test_my_sum_fail(void) {
  const int sum = my_sum(1, -1);
  TEST_ASSERT_EQUAL_INT(0, sum);
}
```
For this demonstration, you can edit the file directly in your browser, and commit the change. In general, you would push changes from a clone of the repository.

### Rerun the workflow

The commited change will automatically trigger a new run of the workflow. You can also manually start a new run as before.

Observe in the output that all tests are now successful.
```
/home/ubuntu/AVH-GetStarted/basic/main.c:57:test_my_sum_pos:PASS
/home/ubuntu/AVH-GetStarted/basic/main.c:58:test_my_sum_neg:PASS
/home/ubuntu/AVH-GetStarted/basic/main.c:59:test_my_sum_fail:PASS
/home/ubuntu/AVH-GetStarted/basic/main.c:60:test_my_sum_zero:PASS
```
## Next steps

[Jenkins?](/iot/cicd/jenkins)

[<-- Return to Learning Path](/iot/cicd/#sections)
