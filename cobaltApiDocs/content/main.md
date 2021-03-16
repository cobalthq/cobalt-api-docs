---
weight: 10
title: API Reference
---

# Introduction

Welcome to the [Cobalt.io](https://cobalt.io) public API docs portal. You can use our REST API to access information on orgs, assets, pentests, findings and events from our database. Our API is currently read-only.

# Authentication

> To authorize, give this a try:

```shell
curl -X GET "https://api.cobalt.io/orgs"
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

Our Living Documentation and API Explorer are located in [Swagger](https://app.swaggerhub.com/apis/CobaltLab/Cobalt_Public_API/1.3.0) and built with the [OpenAPI specification](https://swagger.io/specification/). 
 - With your token copied locally (once you leave the profile page you won't be able to copy it), head to Swagger
 - Make sure to point to Production (i.e. https://api.cobalt.io) from the drop-down 
 - Authorize with your API token
 - From there, you'll want to execute the `/orgs` endpoint (Try it out => Execute)
 - Note the organization `token` 
 - Return back to the Authorize section and add the org `token` and Authorize that as part of your OrgToken (i.e. `X-Org-Token`) header
 - Now, all subsequent requests to `/assets`, `/findings`, `/pentests`, etc will be scoped to your personal API token and the org selected


