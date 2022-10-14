---
weight: 3
title: Authentication
---

# Authentication

Cobalt uses API tokens to allow access to various endpoints. You can create a new Cobalt API token from within your
[Cobalt profile](https://app.cobalt.io/settings/api-token).

Cobalt expects the API token to be included in all API requests to the server in a header that looks like the following:

`Authorization: Bearer YOUR-PERSONAL-API-TOKEN`

<aside class="notice">
You must replace <strong>YOUR-PERSONAL-API-TOKEN</strong> with your personal API token. DO NOT remove the word Bearer.
</aside>

Our Living Documentation and API Explorer are located in [Swagger](https://app.swaggerhub.com/apis/CobaltLab/cobalt-api/)
and built with the [OpenAPI specification](https://swagger.io/specification/).
To explore our API, complete the following steps:

- Create and copy your API token from your [Cobalt profile](https://app.cobalt.io/settings/api-token).
- Go to [Swagger](https://app.swaggerhub.com/apis/CobaltLab/cobalt-api/) and select the green
  _Authorize_ button on the right side of the screen.
- Paste your API token into the `ApiToken` text box.
- Select the green _Authorize_ button below the `ApiToken` input. You should see `Authorized` below
  the `ApiToken` label.
- Close the Available Authorizations dialog box.

Most API calls are scoped to a specific organization, with the `X-Org-Token` header. We include
that header, as needed, in our API calls.

To see which organizations you belong to:

- Search for the `Orgs` endpoint.
- Select the `GET /orgs` operation to expand it.
- Select the _Try it out_ button, and then select the _Execute_ button (note that you do **not**
  need to provide the `X-Org-Token` header here).
- Scroll down to the `Response body`. Copy the `token` associated with your target organization
  (`org`). This is your Org Token. Include it with the `X-Org-Token` header when required.

<aside class="warning">
If your organization uses SAML for authentication with Cobalt, API tokens are not currently disabled when a user is
offboarded from SAML. To disable API access by offboarded personnel, you must manually remove them from your
organization via the "People" tab on the Cobalt platform. Automating this offboarding process is a high-priority issue
for Cobalt and an automated solution will be released as soon as possible.
</aside>
