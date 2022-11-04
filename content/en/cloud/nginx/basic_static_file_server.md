---
processors : ["Neoverse-N1"]
software : ["linux"]
title: "Setup file server"
type: docs
weight: 3
hide_summary: true
description: >
    Learn how to setup a basic file server.
---

## Prerequisites

* Physical machines or cloud nodes with Ubuntu installed.
* An installation of Nginx.

## Setup Basic file server

Follow [this documentation](https://armkeil.blob.core.windows.net/developer/Files/pdf/white-paper/guidelines-for-deploying-nginx-plus-on-aws.pdf) to setup a basic file server.

### Steps in brief

NOTE: The below mentioned steps are used to setup a basic file server.

*  Switch to root user:

```console
sudo su -
```

* Add the following code in **/etc/nginx/nginx.conf**:

```console
user www-data;
worker_processes auto;
worker_rlimit_nofile 1000000;
pid /run/nginx.pid;
events {
 worker_connections 1024;
 accept_mutex off;
 multi_accept off;
}
http {
 ##
 # Basic Settings
 ##
 sendfile on;
 tcp_nopush on;
 tcp_nodelay on;
 keepalive_timeout 75;
 types_hash_max_size 2048;
 include /etc/nginx/mime.types;
 default_type application/octet-stream;

 ##
 # Virtual Host Configs
 ##
 include /etc/nginx/conf.d/*.conf;
 include /etc/nginx/sites-enabled/*;
}
```

* Add the following code in **/etc/nginx/conf.d/default.conf**:

```console
# HTTPS file server
server {
 listen 443 ssl reuseport backlog=60999;
 root /usr/share/nginx/html;
 index index.html index.htm;
 server_name $hostname;
 ssl on;
 ssl_certificate /etc/nginx/ssl/ecdsa.crt;
 ssl_certificate_key /etc/nginx/ssl/ecdsa.key;
 ssl_ciphers ECDHE-ECDSA-AES256-GCM-SHA384;
 location / {
     limit_except GET {
         deny all;
     }
     try_files $uri $uri/ =404;
 }
}
```
Here **$hostname** will be replaced with the DNS of the machine.

NOTE: Follow the [instructions](/content/en/cloud/nginx/key_and_certification.md) to create ECDSA key and certificate.

* Check the configuration for correct syntax and then start the Nginx server using the below commands:

```console
nginx -t -v
systemctl start nginx
```

* To verify the file server is running, open the below URL in a browser. You should see the content of your index.html file displayed:

```console
https://<upstream_ip_dns>/
```
Here <upstream_ip_dns> will be the DNS or IP address of your machine. You will see something like this:

![file_server_screenshot](https://user-images.githubusercontent.com/67620689/194551227-3590f90c-8c58-4f1d-bed6-71527cec7c62.PNG)

NOTE: Before verifying ensure that port 443 is exposed in the security group.

[<-- Return to Learning Path](/content/en/cloud/nginx/#sections)
