# PROJECT UPDATE

This project has migrated to a new hugo template and [new repository](https://github.com/zachlas/arm-software-developers-ads). Please use the new repo for content contributions and see then on the [new URL](https://www.armswdev.tk/)

# Prototyping site for Arm Software Developers

This prototype uses [Docsy](https://www.docsy.dev/), a [Hugo](https://gohugo.io/) theme module for technical documentation sites, providing easy
site navigation, structure, and more. This **Project** uses the Docsy
theme component as a hugo module and provides a skeleton documentation structure for us to demonstrate concepts.

You can find detailed theme instructions in the [Docsy user guide](https://www.docsy.dev/docs/).

## Getting started

To work on the project start by cloing the project and run locally.

```bash
git clone --recurse-submodules https://github.com/jasonrandrews/arm-software-developers.git
```

```bash
npm install
```

You can now edit your own versions of the site’s source files.

To see your changes run the site locally.

## Running the website locally

Building and running the site locally requires a version of [Hugo](https://gohugo.io) and Go. 
You can find out more about how to install Hugo in the
[Getting started](https://www.docsy.dev/docs/getting-started/#prerequisites-and-installation) guide.
The [Installation Prerequisites](https://www.docsy.dev/docs/get-started/docsy-as-module/installation-prerequisites/) is also good.

The required software is Hugo, npm, and golang. 

Once you've made your working copy of the site repo, from the repo root folder, run:

```
hugo server
```

## Develop in [Gitpod](https://www.gitpod.io/)

Instead of installing tools on your local machine, you can develop content directly in Gitpod. 

Install the [Gitpod Chrome Extension](https://chrome.google.com/webstore/detail/gitpod-always-ready-to-co/dodmmooeoklaejobgleioelladacbeki) which installs a Gitpod button in the GitHub project. You can also prefix the URL for the GitHub project (or your fork of the project) with gitpod.io/# 

[Open this repository in Gitpod](https://gitpod.io/#github.com/jasonrandrews/arm-software-developers)

## Building the website 

To build run hugo, it will generate the public/ directory of files to copy to a static webiste hosting service such as AWS S3 bucket setup for static hosting.

```
hugo
```

## Deploy to AWS S3

There is an AWS S3 bucket setup on config.toml to deploy to AWS S3. This is done automatically when commits are made the repository so there is no need to do it manually

The general command to deploy to S3 is:

```
hugo deploy
```

Here are some useful links:

Refer to the file [NOTES.md](NOTES.md) to see some of the details of what has been customized. 

[Docsy user guide](https://docsy.dev/docs)

[Docsy](https://github.com/google/docsy)

[example.docsy.dev](https://example.docsy.dev)

[Hugo theme module](https://gohugo.io/hugo-modules/use-modules/#use-a-module-for-a-theme)
