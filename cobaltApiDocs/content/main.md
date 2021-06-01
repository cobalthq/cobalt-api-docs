---
weight: 10
title: API Reference
---

# Introduction

The [Cobalt](https://cobalt.io) API gives you REST access to Orgs, Assets, Pentests, Findings, and Events, and is currently read-only.

<aside class="notice">
We are actively working to improve the usability of our API and welcome your feedback: <strong>integrations@cobalt.io</strong>
</aside>

# Authentication

> To authorize, give this a try:

```shell
curl https://api.cobalt.io/orgs \
  -H "Authorization: Bearer your-personal-API-token-here"
```

> Make sure to replace `your-personal-API-token-here` with your actual API token.

Cobalt uses API tokens to allow access to various endpoints. You can create a new Cobalt API token from within your [Cobalt profile](https://app.cobalt.io/settings/api-token).

Cobalt expects the API token to be included in all API requests to the server in a header that looks like the following:

`Authorization: Bearer your-personal-API-token-here`

<aside class="notice">
You must replace <code>your-personal-API-token-here</code> with your personal API token.<br>
DO NOT remove the word Bearer.
</aside>

Our Living Documentation and API Explorer are located in [Swagger](https://app.swaggerhub.com/apis/CobaltLab/Cobalt_Public_API/1.3.3) and built with the [OpenAPI specification](https://swagger.io/specification/).
 - With your token copied locally (once you leave the profile page you won't be able to copy it), head to Swagger
 - Make sure to point to Production (i.e. https://api.cobalt.io) from the drop-down
 - Authorize with your API token
 - From there, you'll want to execute the `/orgs` endpoint (Try it out => Execute)
 - Note the org `token`
 - Return back to the Authorize section and add the org `token` and Authorize that as part of your OrgToken (i.e. `X-Org-Token`) header
 - Now, all subsequent requests to `/assets`, `/findings`, `/pentests`, etc will be scoped to your personal API token and the org selected

<aside class="warning">
If your organization uses SAML for authentication with Cobalt, API tokens are not currently disabled
when a user is offboarded from SAML.  To disable API access by offboarded personnel, you must
manually remove them from your organization via the "People" tab on the Cobalt platform.  Automating
this offboarding process is a high-priority issue for Cobalt and a permanent fix will be released as
soon as possible.
</aside>
