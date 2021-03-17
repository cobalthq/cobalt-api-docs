Cobalt Public API Docs
===============================
These docs complement our OpenAPI Swagger docs with walkthroughs and examples of endpoints, fields, and query parameters. You can easily add or edit pages using Markdown from the `cobaltApiDocs/content/` directory, where `main.md` is the entry point. All other pages utilize a `weight` property to indicate where they're nested in navigation.

## Local Development

Install Go + Hugo with Homebrew

```
brew install go
brew install hugo
```

From any site directory (e.g. `exampleSite` or in our case, `cobaltApiDocs`), you can test and deploy changes locally with

```
hugo serve
```

## Hosting

The site uses Netlify's CD pipeline and is hosted at [docs.cobalt.io](https://docs.cobalt.io) using a Cloudflare CNAME pointed at cobalt-api.netlify.app.

[![Netlify Status](https://api.netlify.com/api/v1/badges/b42b3f4e-140b-472d-becf-a0ce06e197d5/deploy-status)](https://app.netlify.com/sites/cobalt-api/deploys)

All commits to `master`, if the build is successful, will be automatically deployed to the production site (usually in < 1 minute).

<br/>

**Deploy previews**
Any pull request against the `master` branch will listen for new commits and is set to auto-build, available for preview before merging (Click Details in the PR Check).


## Origin

**DocuAPI** is a multilingual API documentation theme for [Hugo](http://gohugo.io/). This theme is built on top of the beautiful work of [Robert Lord](https://github.com/lord) and others on the [Slate](https://github.com/slatedocs/slate) project ([Apache 2 License](https://github.com/slatedocs/slate/blob/master/LICENSE)) and is maintained [here](https://github.com/bep/docuapi).


## Use

The client library used to build the ToC does not handle Unicode very well. To get around this in Hugo >= 0.62.2, put this in your site config:

```toml
[markup]
  [markup.goldmark]
    [markup.goldmark.parser]
      autoHeadingIDType = "github-ascii"
```

**Note:** this theme requires Hugo >= 0.56.0 to run. If you want to edit the SCSS styles, you need:

* The extended Hugo version.
* PostCSS CLI (run `npm install` to install requirements)

See the [exampleSite](https://github.com/bep/docuapi/tree/master/exampleSite) and more specific its site [configuration](https://github.com/bep/docuapi/blob/master/exampleSite/config.toml) for the available options.

**Most notable:** This theme will use all the (non drafts) pages in the site and build a single-page API documentation. Using `weight` in the page front matter is the easiest way to control page order.

If you want a different page selection, please provide your own `layouts/index.html` template.

You can customize the look-and-feel by adding your own CSS variables in `assets/scss/docuapi_overrides.scss`. See the exampleSite folder for an example.

## Hooks

You can override the layouts by providing some custom partials:

* `partials/hook_head_end.html` is inserted right before the `head` end tag. Useful for additional styles etc.
* `partials/hook_body_end.html` which should be clear by its name.
* `partials/hook_left_sidebar_start.html` the start of the left sidebar
* `partials/hook_left_sidebar_end.html` the end of the left sidebar
* `partials/hook_left_sidebar_logo.html` the log `img` source

The styles and Javascript import are also put in each partial and as such can be overridden if really needed:

* `partials/styles.html`
* `partials/js.html`
