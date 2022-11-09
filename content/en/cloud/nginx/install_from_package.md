---
processors : ["Neoverse-N1"]
software : ["linux"]
title: "Install Nginx from package"
type: docs
weight: 1
hide_summary: true
description: >
    Learn how to install Nginx from package.
---

## Prerequisites

* Physical machines or cloud nodes with Ubuntu installed.

## Install Nginx from package

Follow [this documentation](https://docs.nginx.com/nginx/admin-guide/installing-nginx/installing-nginx-open-source/#installing-a-prebuilt-ubuntu-package-from-an-ubuntu-repository) to install Nginx from package.

### Steps in brief

* Update the Ubuntu repository information:

```console
apt-get update
```

* Install the package:

```console
apt-get install nginx
```

* Verify the installation:

```console
nginx -v
```

[<-- Return to Learning Path](/content/en/cloud/nginx/#sections)
