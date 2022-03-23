---
weight: 10
title: Tokens
---

# Tokens

## Get All Tokens

```sh
curl -X GET "https://api.cobalt.io/tokens" \
  -H "accept: application/vnd.cobalt.v2+json" \
  -H "Authorization: Bearer your-personal-api-token-here"
```

> The above command returns JSON structured like this:

```json
{
  "pagination": {
    "next_page": null,
    "prev_page": null
  },
  "data": [
    {
      "resource": {
        "id": "api_Dge3LsHMjtX8SGEk4a8nur",
        "last_characters": "9qy7",
        "name": "Your token name",
        "expire_at": null
      }
    }
  ]
}
```

This endpoint retrieves a list of all tokens that belong to you.

### HTTP Request

`GET https://api.cobalt.io/tokens`

### URL Parameters

Parameter | Default | Description
--------- | ------- | -----------
cursor    | N/A     | Used for [pagination](./#pagination), e.g. `https://api.cobalt.io/tokens?cursor=123asdzxc`
limit     | `10`    | If specified, returns only `limit` tokens, e.g. `https://api.cobalt.io/tokens?limit=5`

### Response Fields

| Field             | Description                                         |
|-------------------|-----------------------------------------------------|
| `id`              | The Cobalt ID of the token, an alphanumeric string  |
| `name`            | Name of the API token                               |
| `last_characters` | Last four characters of your token                  |
| `expire_at`       | null (not currently implemented)                    |
