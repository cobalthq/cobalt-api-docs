---
weight: 9
title: Tokens
---

# Tokens

## Get All Tokens

```sh
curl -X GET "https://api.cobalt.io/tokens" \
  -H "Accept: application/vnd.cobalt.v1+json" \
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
 ]
}
```

This endpoint retrieves a list of all tokens that belong to you.

### HTTP Request

`GET https://api.cobalt.io/tokens`

### Response Fields

| Field             | Description                                                                                          |
|-------------------|------------------------------------------------------------------------------------------------------|
| `id`              | A unique ID representing the token. Starts with `api_`                                               |
| `name`            | Name of the API token                                                                                |
| `last_characters` | Last four characters of your token, so that you can recognize tokens even if they have the same name |
| `expire_at`       | null (not currently implemented)                                                                     |
