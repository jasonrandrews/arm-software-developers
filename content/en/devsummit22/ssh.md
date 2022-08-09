---
title: "Setup SSH access without VPN"
linkTitle: "Setup SSH access"
type: docs
toc_hide: true
hide_summary: true
description: >
    Learn how to setup SSH access to your Arm Virtual Hardware instances without the need for VPN. These steps must be done before instantiation.
---
## Overview

In this section we will learn how to setup SSH access to your Arm Virtual Hardware instances without the need for VPN. This requires some initial settings to enable remote access to your Virtual Hardware session. These steps need only be done once, but must be done before launching a Virtual Hardware instance. Full instructions are given [here](https://intercom.help/arm-avh/en/articles/6347261-quick-connect).

## Pre-requisites

* User account for [Arm Virtual Hardware](https://avh.arm.com/)

## Detailed Instructions

### Generate API Token

You will need to generate a unique API token to enable remote access to your Arm Virtual Hardware session.

Click on `PROFILE` in upper-right of your Virtual Hardware browser pane, and then the `API` tab. Click on `GENERATE` to create a token. Copy and paste this to a text editor for future use. Note that the token will only be displayed once. If you need to regenerate, note that a new token will be created, and you will need to update all instances where it is used later.

### Authenticate Rest API with this token

Browse to the `Arm API` page:
```console
https://app.avh.arm.com/api/docs
```
Select `Log in` (under `Authentication` operations) from the side menu. You can use the text Filter if necessary.

In the supplied `EXAMPLE` change `<token>` to the newly generated `API token`, and click `TRY`. You will receive a `RESPONSE` similar to:
```
{
  "token": "VERY_LONG_TOKEN",
  "expiration": "TIMESTAMP"
}
```
Copy the given `VERY_LONG_TOKEN`.

Go to the `Authentication` page from the side menu (note this is different from `Authentication` operations section).\
Enter your `VERY_LONG_TOKEN` into the `api-token` field, and click `SET`. The system will report `Key Applied`.

### Generate and set up SSH Key-Pair

On the [Arm API](https://app.avh.arm.com/api/docs) page, jump to `Get Projects` (use text filter as before if necessary). Click `TRY`, and you will get a `RESPONSE` similar to:
```
  {
    "id": "PROJECT_ID",
    "name": "Default Project",
    "settings": {
      "version": 1,
      "internet-access": true
    },
...
```
Copy the given `PROJECT_ID`. Now jump to `Add Project Authorized Key`, and enter this `PROJECT_ID`.

Open a terminal on your host machine, and enter the following. When prompted, you can leave `passphrase` blank.
```console
ssh-keygen -t ed25519
```
This will generate `id_ed25519.pub`.

In the `Add Project Authorized Key` example JSON file, enter the contents of `id_ed25519.pub` as the `key`.
```
{
  "type": "ssh",
  "label": "My New Key",
  "key": "ssh-ed25519 LONG_STRING user@hostmachine"
}
```
Finally, click on `TRY` to register the key. You are now ready to use SSH with your virtual devices.

### Create new Raspberry Pi instance

Navigate to the Arm Virtual Hardware `DEVICES` view, and observe how many CPU cores you have available in your account. You require `4` to create a new Raspberry Pi instance. If necessary, select the `lighting-app` instance, and click the `trashcan` icon to delete the instance.

Select `CREATE DEVICE`, and create a `Raspberry Pi 4` instance with `Raspberry Pi OS lite`. Give it a meaningful name, for example `RPi SSH`.

When created, go to the `CONNECT` tab and copy the `SSH` command for your instance (this will be unique to your instance). Run this command on your host machine terminal.

## Next Steps

[<-- Return to Workshop Home](/devsummit22/#sections)