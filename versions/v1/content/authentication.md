---
weight: 3
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

<aside class="warning">
If your organization uses SAML for authentication with Cobalt, API tokens are not currently disabled when a user is
offboarded from SAML. To disable API access by offboarded personnel, you must manually remove them from your
organization via the "People" tab on the Cobalt platform. Automating this offboarding process is a high-priority issue
for Cobalt and an automated solution will be released as soon as possible.
</aside>
