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
and built with the [OpenAPI specification](https://swagger.io/specification/).  To explore our API
from Swagger, complete the following steps:

- Create and copy your API token from your [Cobalt profile](https://app.cobalt.io/settings/api-token).
- Go to [Swagger](https://app.swaggerhub.com/apis/CobaltLab/cobalt-api/) and click the green
  _Authorize_ button on the right side of the screen.
- Paste your API token into the `ApiToken` input.
- Click the green _Authorize_ button below the `ApiToken` input.  The word `Authorized` should
  appear underneath the `ApiToken` input.
- Close the dialog box by clicking either _Close_ button.
- Scroll down in the right endpoints column until you see the `Orgs` section.
- Click the `GET /orgs` endpoint to expand it.
- Click the _Try it out_ button, then click the _Execute_ button.
- Scroll down to the `Response body` section.  Depending on how many orgs you belong to, you should
  see one or more `resource` sections within the output.  Each of those sections should contain a
  `token` field.  Select the org you want to experiment with and copy the `token` field value.  This
  is your Org Token.
- Return back to the _Authorize_ section.
- Paste the Org Token into the `OrgToken` input and click the green _Authorize_ button below it.
  The word `Authorized` should appear underneath the `OrgToken` input.
- Close the dialog box again by clicking either _Close_ button.
- All subsequent requests to `/assets`, `/findings`, `/pentests`, etc. will be scoped to your
  personal API token and the organization selected.

<aside class="warning">
If your organization uses SAML for authentication with Cobalt, API tokens are not currently disabled when a user is
offboarded from SAML. To disable API access by offboarded personnel, you must manually remove them from your
organization via the "People" tab on the Cobalt platform. Automating this offboarding process is a high-priority issue
for Cobalt and an automated solution will be released as soon as possible.
</aside>
