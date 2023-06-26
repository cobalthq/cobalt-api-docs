---
weight: 4
title: Organizations
---

# Organizations

## Get All Organizations

```sh
curl -X GET "https://api.cobalt.io/orgs" \
  -H "Accept: application/vnd.cobalt.v2+json" \
  -H "Authorization: Bearer YOUR-PERSONAL-API-TOKEN"
```

> Response Sample

```json
{
  "data": [
    {
      "resource": {
        "id": "or_Uevoq7MyoYsPT9NPc3conL",
        "name": "Acme Corp.",
        "token": "e9d6da*****************************0e8ad"
      },
      "links": {
        "ui": {
          "url": "https://api.cobalt.io/links/eyJ0eXBlIjoic29tZXRoaW5nIiwib3JnU2x1ZyI6ImNvYmFsdCIsInBlbnRlc3RUYWciOiJz="
        }
      }
    },
    {
      "resource": {
        "id": "or_SnUYXDBYd2qbaDSuNRNa5q",
        "name": "Lorem Corp.",
        "token": "f1d6da*****************************0e8ad"
      },
      "links": {
        "ui": {
          "url": "https://api.cobalt.io/links/eyJ0eXBlIjoic29tZXRoaW5nIiwib3JnU2x1ZyI6ImNvYmFsdCIsInBlbnRlc3RUYWciOiJz="
        }
      }
    }
  ],
  "pagination": {
    "next_page": "/orgs?cursor=a1b2c3d4",
    "prev_page": "/orgs?cursor=4d3c2b1a"
  }
}
```

{{% organizations-intro %}}

### HTTP Request

`GET https://api.cobalt.io/orgs`

### Query Parameters

| Name | Default | Description                                                                                                      |
|-----------|---------|------------------------------------------------------------------------------------------------------------------|
| `cursor`  | N/A     | {{% cursor %}} Example: `https://api.cobalt.io/orgs?cursor=a1b2c3d4`                   |
| `limit`   | `10`    | {{% limit %}} Example: `https://api.cobalt.io/orgs?limit=5` |

### Response Parameters

| Name          | Description                                                                              |
|----------------|------------------------------------------------------------------------------------------|
| `id`           | {{% org-id %}}                             |
| `name`         | {{% org-name %}}                                                             |
| `token`        | {{% org-token-definition %}}                                   |
| `links.ui.url` | {{% org-links-ui-url %}} |
