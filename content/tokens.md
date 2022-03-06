---
weight: 9
title: Tokens
---

# Tokens

## Get All Tokens

```sh
curl -X GET "https://api.cobalt.io/tokens" \
  -H "accept: application/vnd.cobalt.v1+json" \
  -H "Authorization: Bearer your-personal-api-token-here" 
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "resource": {
        "id": "34",
        "last_characters": "9qy7",
        "name": "my token",
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

| Field             | Description                                                  |
|-------------------|--------------------------------------------------------------|
| `id`              | Integer field used in the POST request to refresh your token |
| `name`            | Your API token name                                          |
| `last_characters` | Last four characters of your token for recall                |
| `expire_at`       | null (not currently implemented)                             |
