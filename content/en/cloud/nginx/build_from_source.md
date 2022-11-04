---
processors : ["Neoverse-N1"]
software : ["linux"]
title: "Build Nginx from source"
type: docs
weight: 2
hide_summary: true
description: >
    Learn how to build Nginx from the source.
---

## Prerequisites

* Physical machines or cloud nodes with Ubuntu installed.
* Install wget, unzip, and mercurial using the following command:
```console
apt-get install wget unzip mercurial -y
```

## Build Nginx from source

Follow [this documentation](http://nginx.org/en/docs/configure.html) to build Nginx from the source.

### Steps in brief

NOTE: The below mentioned steps are used to build Nginx from source in Ubuntu.

* Download and extract the latest source code of PCRE from [here](http://www.pcre.org/), below we show 10.39 as an example. The rest is done by Nginx's ./configure and make:

```console
wget https://github.com/PCRE2Project/pcre2/releases/download/pcre2-10.39/pcre2-10.39.zip
unzip pcre2-10.39.zip
```

* The zlib library distribution (version 1.1.3 - 1.2.11) needs to be downloaded from the [zlib](https://zlib.net/fossils/) site and extracted. The rest is done by Nginx's ./configure and make:

```console
wget https://zlib.net/fossils/zlib-1.2.11.tar.gz
tar -xvf zlib-1.2.11.tar.gz
```

* Clone the Nginx source code:

```console
hg clone http://hg.nginx.org/nginx
cd nginx/
```

* Install the following dependencies:

```console
apt-get install gcc libssl-dev make -y
```

* The build is configured using the **configure** command. It defines various aspects of the system, including the methods Nginx is allowed to use for connection processing. In the end, it creates a Makefile.

```console
./auto/configure --prefix=/usr/share/nginx --sbin-path=/usr/sbin/nginx --conf-path=/etc/nginx/nginx.conf --http-log-path=/var/log/nginx/access.log --error-log-path=/var/log/nginx/error.log --lock-path=/var/lock/nginx.lock --pid-path=/run/nginx.pid --with-http_ssl_module --modules-path=/etc/nginx/modules --with-stream=dynamic --with-pcre=../pcre2-10.39 --with-zlib=../zlib-1.2.11
```

There are many configuration options available in Nginx. To find all the configuration options available in Nginx check [here](http://nginx.org/en/docs/configure.html).

* After configuration, Nginx is compiled and installed using make:

```console
make
make install
```

* To verify if Nginx is installed or not check its version by using the command:

```console
nginx -v
```

* To enable the systemd service, create a file named **/lib/systemd/system/nginx.service** and add the below script in the file.

```console
[Unit]
Description=The NGINX HTTP and reverse proxy server
After=syslog.target network-online.target remote-fs.target nss-lookup.target
Wants=network-online.target

[Service]
Type=forking
PIDFile=/run/nginx.pid
ExecStartPre=/usr/sbin/nginx -t
ExecStart=/usr/sbin/nginx
ExecReload=/usr/sbin/nginx -s reload
ExecStop=/bin/kill -s QUIT $MAINPID
PrivateTmp=true

[Install]
WantedBy=multi-user.target
```

* Now Nginx can be managed using systemd.

```console
systemctl start nginx
```

[<-- Return to Learning Path](/content/en/cloud/nginx/#sections)
