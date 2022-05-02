# Prototyping site for Arm Software Deverlopers

[Docsy][] is a [Hugo theme module][] for technical documentation sites, providing easy
site navigation, structure, and more. This **Project** uses the Docsy
theme component as a hugo module and provides a skeleton documentation structure for us to demonstrate concepts.

You can find detailed theme instructions in the [Docsy user guide][].

The original Docsy Example Project this was started from is hosted on [Netlify][] at [example.docsy.dev][].

## Getting started

To get started clone the project and run locally.

```bash
git clone --recurse-submodules https://github.com/jasonrandrews/arm-software-developers.git
```

You can now edit your own versions of the site’s source files.

To build for deployment in AWS A3 you need to install `PostCSS`

```bash
npm install
```

## Running the website locally

Building and running the site locally requires a version of [Hugo](https://gohugo.io) and Go. 
You can find out more about how to install Hugo in the
[Getting started](https://www.docsy.dev/docs/getting-started/#prerequisites-and-installation) guide.
The [Installation Prerequisites](https://www.docsy.dev/docs/get-started/docsy-as-module/installation-prerequisites/) is also good.

Once you've made your working copy of the site repo, from the repo root folder, run:

```
hugo server
```

## Building the website 

To build run hugo, it will generate the public/ directory of files to copy to a static webiste hosting service such as AWS S3 bucket setup for static hosting.

```
hugo
```

## Deploy to AWS S3

There is an AWS S3 bucket setup on config.toml to deploy to S3, but needs AWS credentials to work. 

```
hugo deploy
```

## Troubleshooting

As you run the website locally, you may run into the following error:

```
➜ hugo server

INFO 2021/01/21 21:07:55 Using config file: 
Building sites … INFO 2021/01/21 21:07:55 syncing static files to /
Built in 288 ms
Error: Error building site: TOCSS: failed to transform "scss/main.scss" (text/x-scss): resource "scss/scss/main.scss_9fadf33d895a46083cdd64396b57ef68" not found in file cache
```

This error occurs if you have not installed the extended version of Hugo.
See this [section](https://www.docsy.dev/docs/get-started/docsy-as-module/installation-prerequisites/#install-hugo) of the user guide for instructions on how to install Hugo.

Or you may encounter the following error:

```
➜ hugo server

Error: failed to download modules: binary with name "go" not found
```

This error occurs if you have not installed the `go` programming language on your system.
See this [section](https://www.docsy.dev/docs/get-started/docsy-as-module/installation-prerequisites/#install-go-language) of the user guide for instructions on how to install `go`.

Here are some useful links:

[Docsy user guide](https://docsy.dev/docs)

[Docsy](https://github.com/google/docsy)

[example.docsy.dev](https://example.docsy.dev)

[Hugo theme module](https://gohugo.io/hugo-modules/use-modules/#use-a-module-for-a-theme)
