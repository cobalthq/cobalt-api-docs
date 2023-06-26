---
weight: 12
title: Tokens
---

# Tokens

## Get All Tokens

```sh
curl -X GET "https://api.cobalt.io/tokens" \
  -H "Accept: application/vnd.cobalt.v2+json" \
  -H "Authorization: Bearer YOUR-PERSONAL-API-TOKEN"
```

> Response Sample

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

Returns all [personal API tokens](.#personal-api-token) that belong to your account.

### HTTP Request

`GET https://api.cobalt.io/tokens`

### Query Parameters

| Name | Default | Description                                                                                                 |
|-----------|---------|-------------------------------------------------------------------------------------------------------------|
| `cursor`  | N/A     | {{% cursor %}} Example: `https://api.cobalt.io/tokens?cursor=a1b2c3d4`            |
| `limit`   | `10`    | {{% limit %}} Example: `https://api.cobalt.io/tokens?limit=5` |

### Response Parameters

| Name             | Description                                                                                          |
|-------------------|------------------------------------------------------------------------------------------------------|
| `id`              | {{% token-id %}}                                               |
| `name`            | {{% token-name %}}                                                                                |
| `last_characters` | {{% token-last-characters %}} |
| `expire_at`       | {{% token-expire-at %}}                                                                     |

## Refresh Token

```sh
curl -X POST "https://api.cobalt.io/tokens/YOUR-TOKEN-ID/refresh" \
  -H "Accept: application/vnd.cobalt.v2+json" \
  -H "Authorization: Bearer YOUR-PERSONAL-API-TOKEN" \
  -H "Idempotency-Key: A-UNIQUE-IDENTIFIER-TO-PREVENT-UNINTENTIONAL-DUPLICATION"
```

> Response Sample

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

{{% refresh-token-intro %}}

### HTTP Request

`POST https://api.cobalt.io/tokens/YOUR-TOKEN-ID/refresh`

### Response Parameters

| Name       | Description                                                           |
|-------------|-----------------------------------------------------------------------|
| `id`        | {{% token-id %}}            |
| `secret`    | {{% token-secret %}} |
| `name`      | {{% token-name %}}                                                |
| `expire_at` | {{% token-expire-at %}}                                      |
