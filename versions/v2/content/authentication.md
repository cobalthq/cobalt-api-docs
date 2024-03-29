---
weight: 4
title: Authentication
---

# Authentication

Cobalt uses API tokens to allow access to various endpoints. You can create a new Cobalt API token from within your
<a href='https://app.cobalt.io/settings/api-token' rel='nofollow' target='_new'>Cobalt profile</a>.

Cobalt expects the API token to be included in all API requests to the server in a header that looks like the following:

`Authorization: Bearer YOUR-PERSONAL-API-TOKEN`

<aside class="notice">
You must replace <strong>YOUR-PERSONAL-API-TOKEN</strong> with your personal API token. DO NOT remove the word Bearer.
</aside>

Most API calls are scoped to a specific organization, with the `X-Org-Token` header. We include that header, as needed,
in our API calls.

To see which organizations you belong to:

- [Send a GET request](./#get-all-organizations) to the `/orgs` endpoint.
- Copy the `token` attribute associated with your target organization from response.
- Include it as a header (`X-Org-Token`) to your requests when required.

<aside class="warning">
If your organization uses SAML for authentication with Cobalt, API tokens are not currently disabled when a user is
offboarded from SAML. To disable API access by offboarded personnel, you must manually remove them from your
organization via the "People" tab on the Cobalt platform. Automating this offboarding process is a high-priority issue
for Cobalt and an automated solution will be released as soon as possible.
</aside>
