---
weight: 15
title: DAST Targets
---

# DAST Targets

## Get All DAST Targets

```sh
curl -X GET "https://api.us.cobalt.io/dast/targets" \
  -H "Accept: application/vnd.cobalt.v2+json" \
  -H "Authorization: Bearer YOUR-PERSONAL-API-TOKEN" \
  -H "X-Org-Token: YOUR-V2-ORGANIZATION-TOKEN"
```

> The above command returns JSON structured like this:

```json
{
  "pagination": {
    "next_page": "/resource?cursor=123asdzxc",
    "prev_page": "/resource?cursor=123asdzxc"
  },
  "data": [
    {
      "resource": {
        "id": "dt_GZgcehapJUNh6mjNuqsE4T",
        "name": "My DAST Target",
        "url": "https://myapp.local",
        "enabled": true
      }
    }
  ]
}
```

This endpoint retrieves a list of all DAST Targets that belong to the organization specified in the `X-Org-Token` header.

### HTTP Request

`GET https://api.us.cobalt.io/dast/targets`

### URL Parameters

| Parameter          | Default | Description  |
|--------------------|---------|-----------------|
| `cursor`      | N/A     | Used for [pagination](./#pagination). Example: `https://api.us.cobalt.io/dast/targets?cursor=a1b2c3d4` |
| `limit`       | `10`    | If specified, returns only a specified amount of targets. Example: `https://api.us.cobalt.io/dast/targets?limit=5`|

### Response Fields

| Field           | Description                                                                         |
|-----------------|-------------------------------------------------------------------------------------|
| `id`      | A unique ID representing the DAST target. Starts with `dt_`                             |
| `name`    | The name of the returned DAST target.                                                  |
| `url`     | The URL of the returns DAST target              |
| `enabled` | A boolean flag specifying if the DAST target is enabled                                |

## Get a DAST Target

```sh
curl -X GET "https://api.us.cobalt.io/dast/targets/YOUR-DAST-TARGET-IDENTIFIER" \
  -H "Accept: application/vnd.cobalt.v2+json" \
  -H "Authorization: Bearer YOUR-PERSONAL-API-TOKEN" \
  -H "X-Org-Token: YOUR-V2-ORGANIZATION-TOKEN"
```

> The above command returns JSON structured like this:

```json
{
  "resource": {
    "id": "dt_GZgcehapJUNh6mjNuqsE4T",
    "name": "My DAST Target",
    "url": "https://myapp.local",
    "enabled": true
  }
}
```

This endpoint retrieves a specific DAST Target that belongs to the organization specified in the `X-Org-Token` header.

### HTTP Request

`GET https://api.us.cobalt.io/dast/targets/YOUR-DAST-TARGET-IDENTIFIER`

### Response Fields

| Field           | Description                                                                         |
|-----------------|-------------------------------------------------------------------------------------|
| `id`      | A unique ID representing the DAST target. Starts with `dt_`                             |
| `name`    | The name of the returned DAST target.                                                  |
| `url`     | The URL of the returns DAST target              |
| `enabled` | A boolean flag specifying if the DAST target is enabled                                |
