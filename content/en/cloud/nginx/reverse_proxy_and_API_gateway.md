---
processors : ["Neoverse-N1"]
software : ["linux"]
title: "Setup Reverse Proxy and API Gateway"
type: docs
weight: 4
hide_summary: true
description: >
    Learn how to setup a reverse proxy and an API gateway.
---

## Prerequisites

* Physical machines or cloud nodes with Ubuntu installed.
* An installation of Nginx.
* Setup a [basic file server](/content/en/cloud/nginx/basic_static_file_server.md).

NOTE: Here we have created 2 upstream file servers that will be behind the reverse proxy or API Gateway. You can create as many upstream file servers as you wish.

## Setup Reverse Proxy and API Gateway

Follow [this documentation](https://armkeil.blob.core.windows.net/developer/Files/pdf/white-paper/guidelines-for-deploying-nginx-plus-on-aws.pdf) to setup Reverse Proxy and API Gateway.

### Steps in brief

NOTE: The below mentioned steps are used to setup Reverse Proxy and API Gateway.

* Switch to root user:

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
 keepalive_requests 1000000000;
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
# Upstreams for https
upstream ssl_file_server_com {
 server <private_ip_1>:443;
 server <private_ip_2>:443;
 keepalive 1024;
}

# HTTPS reverse proxy and API Gateway
server {
 listen 443 ssl reuseport backlog=60999;
 root /usr/share/nginx/html;
 index index.html index.htm;
 server_name $hostname;
 ssl on;
 ssl_certificate /etc/nginx/ssl/ecdsa.crt;
 ssl_certificate_key /etc/nginx/ssl/ecdsa.key;
 ssl_ciphers ECDHE-ECDSA-AES256-GCM-SHA384;

 # API Gateway Path
 location ~ ^/api_old/.*$ {
 limit_except GET {
 deny all;
 }
 rewrite ^/api_old/(.*)$ /api_new/$1 last;
 }
 location /api_new {
 internal;
 proxy_pass https://ssl_file_server_com;
 proxy_http_version 1.1;
 proxy_set_header Connection "";
 }

 # Reverse Proxy Path
 location / {
 limit_except GET {
 deny all;
 }
 proxy_pass https://ssl_file_server_com;
 proxy_http_version 1.1;
 proxy_set_header Connection "";
 }
}
```
Here **$hostname** will be replaced with the DNS of the machine and <private_ip_1> and <private_ip_2> are the private IP of the upstream file servers that we have created.

NOTE: Follow the [instructions](/content/en/cloud/nginx/key_and_certification.md) to create ECDSA key and certificate

* Check the configuration for correct syntax run and then start Nginx server using the below commands:

```console
nginx -t -v
systemctl start nginx
```

* To verify the reverse proxy and api gateway:

Run the following commands on the upstreams to generate the files that will be served:
```console
# Create 1kb file in RP use case directory
dd if=/dev/urandom of=/usr/share/nginx/html/1kb bs=1024 count=1
# Copy files into the APIGW use case directory
mkdir -p /usr/share/nginx/html/api_new
cp /usr/share/nginx/html/1kb /usr/share/nginx/html/api_new
```

* To verify the reverse proxy server is running open the URL in your browser and now the file will be downloaded from RP use case directory:

```console
https://<rp_apigw_ip_dns>/1kb
```
Here <rp_apigw_ip_dns> is the DNS name or IP address of the machine.

* Now open the URL in your browser and now the file will be downloaded from APIGW use case directory:

```console
https://<rp_apigw_ip_dns>/api_old/1kb
```
Here <rp_apigw_ip_dns> is the DNS name or IP address of the machine.

NOTE: Before verifying ensure that port 443 is exposed in the security group.

[<-- Return to Learning Path](/content/en/cloud/nginx/#sections)
