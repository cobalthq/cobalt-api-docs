---
weight: 3
title: Authentication
---

# Authentication

> To authorize, give this a try:

```sh
curl https://api.cobalt.io/orgs \
  -H "Authorization: Bearer YOUR_PERSONAL_API_TOKEN"
```

> Make sure to replace `YOUR_PERSONAL_API_TOKEN` with your actual API token.

Cobalt uses API tokens to allow access to various endpoints. You can create a new Cobalt API token from within your
[Cobalt profile](https://app.cobalt.io/settings/api-token).

Cobalt expects the API token to be included in all API requests to the server in a header that looks like the following:

`Authorization: Bearer YOUR_PERSONAL_API_TOKEN`

<aside class="notice">
You must replace <strong>YOUR_PERSONAL_API_TOKEN</strong> with your personal API token. DO NOT remove the word Bearer.
</aside>

<aside class="warning">
If your organization uses SAML for authentication with Cobalt, API tokens are not currently disabled
when a user is offboarded from SAML. To disable API access by offboarded personnel, you must
manually remove them from your organization via the "People" tab on the Cobalt platform. Automating
this offboarding process is a high-priority issue for Cobalt and an automated solution will be
released as soon as possible.
</aside>

## API V1

Our Living Documentation and API Explorer are located in [Swagger](https://app.swaggerhub.com/apis/CobaltLab/cobalt-api/)
and built with the [OpenAPI specification](https://swagger.io/specification/).

- With your token copied locally (once you leave the profile page you won't be able to copy it), head to Swagger
- Make sure to point to Production (i.e. `https://api.cobalt.io`) from the drop-down
- Authorize with your API token
- From there, you'll want to execute the `/orgs` endpoint (Try it out => Execute)
- Note the org `token`
- Return back to the Authorize section and add the org `token` and Authorize that as part of your OrgToken
  (i.e. `X-Org-Token`) header
- Now, all subsequent requests to `/assets`, `/findings`, `/pentests`, etc will be scoped to your personal API token
  and the org selected

## API V2

Currently only `v1` of the Cobalt API is supported in Swagger.  You'll need to manually call the
`/orgs` endpoint with an `Accept` header set to `application/vnd.cobalt.v2+json`.  This will ensure
that you get an org `token` compatible with `v2` of the API.

<aside class="notice">
Org `tokens` are incompatible between `v1` and `v2` of the Cobalt API.  You <strong>must</strong>
ensure that you use the proper version of the org `token`.
</aside>
