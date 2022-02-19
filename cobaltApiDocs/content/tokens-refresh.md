---
weight: 17
title: Refresh Token
---

## Refresh Token

```sh
curl -X POST "https://api.cobalt.io/tokens/token-id-here/refresh" \
  -H "accept: application/vnd.cobalt.v1+json" \
  -H "Authorization: Bearer your-personal-api-token-here" 
```

> The above command returns JSON structured like this:

```json
{
  "id": "40",
  "secret": "your-new-personal-API-token-here",
  "expire_at": null
}
```

You can obtain a new token with a POST request to the token refresh endpoint, referencing the token id fetched from the
GET tokens endpoint.

For example, with a valid API token you would first make a GET request to list your tokens, note your current token
`id` in this response, and then use that `id` in the refresh endpoint URL. This will give you a new token back as
`secret` - note it, as your old token will no longer work.

If you've forgotten your token, you can always re-authenticate in the Cobalt web app, go to your
<a href="https://app.cobalt.io/settings/api-token" rel="nofollow">profile</a>, revoke and generate a new token.

### HTTP Request

`POST https://api.cobalt.io/tokens/token-id-here/refresh`

### Fields

| Field       | Description
|-------------|---------------------------------------------------------------|
| `id`        | Your new API token id                                         |
| `secret`    | Your new personal API token - note it for future API requests |
| `expire_at` | null (not currently implemented)                              |
