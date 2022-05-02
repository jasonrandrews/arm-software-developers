# Docsy Example

[Docsy][] is a [Hugo theme module][] for technical documentation sites, providing easy
site navigation, structure, and more. This **Docsy Example Project** uses the Docsy
theme component as a hugo module and provides a skeleton documentation structure for you to use.
You can clone/copy this project and edit it with your own content, or use it as an example.

In this project, the Docsy theme component is pulled in as a Hugo module, together with other module dependencies:

```bash
$ hugo mod graph
hugo: collected modules in 566 ms
hugo: collected modules in 578 ms
github.com/google/docsy-example github.com/google/docsy@v0.2.0
github.com/google/docsy-example github.com/google/docsy/dependencies@v0.2.0
github.com/google/docsy/dependencies@v0.2.0 github.com/twbs/bootstrap@v4.6.1+incompatible
github.com/google/docsy/dependencies@v0.2.0 github.com/FortAwesome/Font-Awesome@v0.0.0-20210804190922-7d3d774145ac
```

You can find detailed theme instructions in the [Docsy user guide][].

This Docsy Example Project is hosted on [Netlify][] at [example.docsy.dev][].
You can view deploy logs from the [deploy section of the project's Netlify
dashboard][deploys], or this [alternate dashboard][].

This is not an officially supported Google product. This project is currently maintained.

## Using the Docsy Example Project as a template

A simple way to get started is to use this project as a template, which gives you a site project that is set up and ready to use. To do this: 

1. Click **Use this template**.

2. Select a name for your new project and click **Create repository from template**.

3. Make your own local working copy of your new repo using git clone, replacing https://github.com/me/example.git with your repo’s web URL:

```bash
git clone --depth 1 https://github.com/jasonrandrews/arm-software-developers.git
```

You can now edit your own versions of the site’s source files.

If you want to do SCSS edits and want to publish these, you need to install `PostCSS`

```bash
npm install
```

## Running the website locally

Building and running the site locally requires a recent `extended` version of [Hugo](https://gohugo.io).
You can find out more about how to install Hugo for your environment in our
[Getting started](https://www.docsy.dev/docs/getting-started/#prerequisites-and-installation) guide.

Once you've made your working copy of the site repo, from the repo root folder, run:

```
hugo server
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


[alternate dashboard]: https://app.netlify.com/sites/goldydocs/deploys
[deploys]: https://app.netlify.com/sites/docsy-example/deploys
[Docsy user guide]: https://docsy.dev/docs
[Docsy]: https://github.com/google/docsy
[example.docsy.dev]: https://example.docsy.dev
[Hugo theme module]: https://gohugo.io/hugo-modules/use-modules/#use-a-module-for-a-theme
[Netlify]: https://netlify.com
