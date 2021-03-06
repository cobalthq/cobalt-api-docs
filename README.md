Cobalt API Docs
===============================
[![Netlify Status](https://api.netlify.com/api/v1/badges/0506a95f-525c-4751-be84-49fc892edf7f/deploy-status)](https://app.netlify.com/sites/cobalt-public-api/deploys)
![](https://github.com/cobalthq/cobalt-public-api-docs/workflows/build/badge.svg)

These docs complement our OpenAPI Swagger docs with walkthroughs and examples of endpoints, fields, and query
parameters. You can easily add or edit pages using Markdown from the `content/` directory. All pages utilize a `weight`
property to indicate where they're nested in navigation.

Cobalt API docs have been created with [hugo](https://github.com/gohugoio/hugo) and [docuapi](https://github.com/bep/docuapi).

## Requirements

- Install hugo:

  ```sh
  brew install hugo
  ```

- Or update if you already have it installed:

  ```sh
  brew update && brew upgrade hugo
  ```

- Install `markdownlint-cli` to check markdown files against some common rules:

  ```sh
  brew install markdownlint-cli
  ```

## Local Development

- Build site and run server:

  ```sh
  # V1
  hugo server --config=versions/v1/config.yaml -D

  # V2
  hugo server --config=versions/v2/config.yaml -D
  ```

- Check markdown files with `markdownlint-cli`:

  ```sh
  markdownlint -c .markdownlint.yaml versions
  ```

## Dependencies

Dependencies in the repository are managed with Go Modules. If you ever need to update the theme manually (probably
you won't, as Dependabot will do it for you) run the following:

```sh
go get github.com/bep/docuapi/v2
```

You will need to have [Go](https://go.dev/dl/) installed for this.

## Hosting

The site uses Netlify's CD pipeline and is hosted at [docs.cobalt.io](https://docs.cobalt.io) using a Cloudflare CNAME
pointed at [cobalt-public-api.netlify.app](https://cobalt-public-api.netlify.app).

## Deployment

All commits to `main`, if the build is successful, will be automatically deployed to the production site (usually
in < 1 minute).

**Deploy previews**

Any pull request against the `main` branch will listen for new commits and is set to auto-build, available for
preview before merging (Click Details in the PR Check).

## Troubleshooting

If you get `found no layout file for "HTML" for kind "page"` warning when you start the server, you can clean up asset
caches by running `hugo mod clean`.
