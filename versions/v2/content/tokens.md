---
weight: 30
title: Tokens
---

# Tokens

## Get All Tokens

```sh
curl -X GET "https://api.us.cobalt.io/tokens" \
  -H "Accept: application/vnd.cobalt.v2+json" \
  -H "Authorization: Bearer YOUR-PERSONAL-API-TOKEN"
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "resource": {
        "id": "api_Dge3LsHMjtX8SGEk4a8nux",
        "last_characters": "redacted",
        "name": "Lorem ipsum",
        "expire_at": null
      }
    }
  ],
  "pagination": {
    "next_page": null,
    "prev_page": null
  }
}
```

This endpoint retrieves a list of all tokens that belong to you.

### HTTP Request

`GET https://api.us.cobalt.io/tokens`

### URL Parameters

| Parameter | Default | Description                                                                                              |
|-----------|---------|----------------------------------------------------------------------------------------------------------|
| `cursor`  | N/A     | Used for [pagination](./#pagination). Example: `https://api.us.cobalt.io/tokens?cursor=a1b2c3d4`            |
| `limit`   | `10`    | If specified, returns only a specified amount of tokens. Example: `https://api.us.cobalt.io/tokens?limit=5` |

### Response Fields

| Field             | Description                                            |
|-------------------|--------------------------------------------------------|
| `id`              | A unique ID representing the token. Starts with `api_` |
| `name`            | Name of the API token                                  |
| `last_characters` | This property is deprecated. Do not use it.            |
| `expire_at`       | null (not currently implemented)                       |

## Refresh Token

```sh
curl -X POST "https://api.us.cobalt.io/tokens/YOUR-TOKEN-ID/refresh" \
  -H "Accept: application/vnd.cobalt.v2+json" \
  -H "Authorization: Bearer YOUR-PERSONAL-API-TOKEN"
```

> The above command returns JSON structured like this:

```json
{
  "resource": {
    "id": "api_Dge3LsHMjtX8SGEk4a8nux",
    "secret": "YOUR-NEW-PERSONAL-API-TOKEN",
    "name": "Lorem ipsum",
    "expire_at": null
  }
}
```

You can revoke an existing token and issue a new one with the same name by making a POST request to the token refresh
endpoint.

Process:

- Make a GET request to the `/tokens` endpoint and note the `id` of the token you would like to refresh.
- Make a POST request to the `/tokens/YOUR-TOKEN-ID/refresh` endpoint using the token `id` obtained in the step above.
- The new token will be contained in the `secret` field of the response. Note this value. Your old token will no longer
  work.

If you've forgotten your token, you can always re-authenticate in the Cobalt web app.
Go to your <a href='https://app.cobalt.io/settings/api-token' rel='nofollow' target='_new'>profile</a>,
revoke the old token you've forgotten, and generate a new token.

### HTTP Request

`POST https://api.us.cobalt.io/tokens/YOUR-TOKEN-ID/refresh`

### Response Fields

| Field       | Description                                                           |
|-------------|-----------------------------------------------------------------------|
| `id`        | A unique ID representing the new token. Starts with `api_`            |
| `secret`    | Your new personal API token. Keep it safe and don't share with anyone |
| `name`      | Name of your API token                                                |
| `expire_at` | null (not currently implemented)                                      |
