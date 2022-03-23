---
weight: 11
title: Refresh Token
---

## Refresh Token

```sh
curl -X POST "https://api.cobalt.io/tokens/token-id-here/refresh" \
  -H "accept: application/vnd.cobalt.v2+json" \
  -H "Authorization: Bearer your-personal-api-token-here" \
  -H "Mutation-Check: unique-identifier-to-prevent-unintentional-duplication"
```

> The above command returns JSON structured like this:

```json
{
  "resource": {
    "id": "api_Dge3LsHMjtX8SGEk4a8nur",
    "secret": "your-new-personal-API-token-here",
    "name": "Your token name",
    "expire_at": null
  }
}
```

You can revoke an existing token and issue a new one with the same name by making a POST request to the token refresh endpoint.

Process:

* Make a GET request to the `/tokens` endpoint and note the `id` of the token you would like to refresh.
* Make a POST request to the `/tokens/ID/refresh` endpoint using the token `id` obtained in the step above.
* The new token will be contained in the `secret` field of the response. Note this value. Your old token will no longer work.

If you've forgotten your token, you can always re-authenticate in the Cobalt web app.
Go to your [profile](https://app.cobalt.io/settings/api-token),
revoke the old token you've forgotten, and generate a new token.

### HTTP Request

`POST https://api.cobalt.io/tokens/token-id-here/refresh`

### Response Fields

| Field       | Description
|-------------|---------------------------------------------------------------|
| `id`        | The Cobalt ID of the new token, an alphanumeric string        |
| `secret`    | Your new personal API token                                   |
| `name`      | Name of the token                                             |
| `expire_at` | null (not currently implemented)                              |
