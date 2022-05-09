---
weight: 3
title: Authentication
---

# Authentication

> To authorize, give this a try:

```sh
curl https://api.cobalt.io/orgs \
  -H "Authorization: Bearer YOUR-PERSONAL-API-TOKEN"
```

> Make sure to replace `YOUR-PERSONAL-API-TOKEN` with your actual API token.

Cobalt uses API tokens to allow access to various endpoints. You can create a new Cobalt API token from within your
[Cobalt profile](https://app.cobalt.io/settings/api-token).

Cobalt expects the API token to be included in all API requests to the server in a header that looks like the following:

`Authorization: Bearer YOUR-PERSONAL-API-TOKEN`

<aside class="notice">
You must replace <strong>YOUR-PERSONAL-API-TOKEN</strong> with your personal API token. DO NOT remove the word Bearer.
</aside>

Our Living Documentation and API Explorer are located in [Swagger](https://app.swaggerhub.com/apis/CobaltLab/cobalt-api/)
and built with the [OpenAPI specification](https://swagger.io/specification/).

- Create and copy your token from your [Cobalt profile](https://app.cobalt.io/settings/api-token).
- Go to [Swagger](https://app.swaggerhub.com/apis/CobaltLab/cobalt-api/) and click the _Authorize_ button.
- Paste your token into the `ApiKeyAuth` input.
- Call the `/orgs` endpoint (Try it out => Execute).
- Copy the `token` value from response body.
- Return back to the _Authorize_ section and add the copied organization `token` into the `OrgToken` input field, and
  click to _Authorize_ button again.
- Now, all subsequent requests to `/assets`, `/findings`, `/pentests`, etc. will be scoped to your personal API token
  and the organization selected.

<aside class="warning">
If your organization uses SAML for authentication with Cobalt, API tokens are not currently disabled when a user is
offboarded from SAML. To disable API access by offboarded personnel, you must manually remove them from your
organization via the "People" tab on the Cobalt platform. Automating this offboarding process is a high-priority issue
for Cobalt and an automated solution will be released as soon as possible.
</aside>
