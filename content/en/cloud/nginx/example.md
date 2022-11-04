---
processors : ["Neoverse-N1"]
software : ["linux"]
title: "Verifying Nginx setup with wget and curl"
type: docs
weight: 5
hide_summary: true
description: >
    Learn how to wget a file from server and curl to retrieve a webpage.
---

## Prerequisites

* Physical machines or cloud nodes with Ubuntu installed(Client instance).
* Setup two [basic file server(Upstreams)](/content/en/cloud/nginx/basic_static_file_server.md).
* Setup a [Reverse Proxy and API gateway(RP/APIGW)](/content/en/cloud/nginx/reverse_proxy_and_API_gateway.md).

## To wget a file from the server

### Steps in brief

* Create a file in the upstreams in /usr/share/nginx/html folder:

```console
cd /usr/share/nginx/html
cat > /usr/share/nginx/html/file.txt
Hi this a text file //Write the content in the file
```

* If the Nginx was running before file creation then restart it on upstreams and RP/APIGW using the command:

```console
systemctl restart nginx
```

* Now to wget run the following command in the client instance:

```console
wget https://<ip_dns>/<file_name> --no-check-certificate
```

Here <ip_dns> is the DNS of the RP/APIGW instance.

## To curl to retrieve a webpage

### Steps in brief

* As we have created upstreams there will be already a file name index.html. Now run the following command in the client instance:

```console
curl -k https://<ip_dns>/index.html
```

Here <ip_dns> is the DNS of the RP/APIGW instance.

NOTE: If you want you can create a new html file in /usr/share/nginx/html folder in upstream instances. Then restart the Nginx on upstreams and RP/APIGW if running before file creation.

[<-- Return to Learning Path](/content/en/cloud/nginx/#sections)
