---
weight: 10
title: Tokens
---

# Tokens

## Get All Tokens

```sh
curl -X GET "https://api.cobalt.io/tokens" \
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
        "last_characters": "9qy7",
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

`GET https://api.cobalt.io/tokens`

### URL Parameters

| Parameter | Default | Description                                                                                          |
|-----------|---------|------------------------------------------------------------------------------------------------------|
| `cursor`  | N/A     | Used for [pagination](./#pagination), e.g. `https://api.cobalt.io/tokens?cursor=a1b2c3d4`            |
| `limit`   | `10`    | If specified, returns only a specified amount of tokens, e.g. `https://api.cobalt.io/tokens?limit=5` |

### Response Fields

| Field             | Description                                                                                          |
|-------------------|------------------------------------------------------------------------------------------------------|
| `id`              | A unique ID representing the token. Starts with `api_`                                               |
| `name`            | Name of the API token                                                                                |
| `last_characters` | Last four characters of your token, so that you can recognize tokens even if they have the same name |
| `expire_at`       | null (not currently implemented)                                                                     |
