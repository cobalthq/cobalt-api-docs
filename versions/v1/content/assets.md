---
weight: 5
title: Assets
---

# Assets

## Get All Assets

```sh
curl -X GET "https://api.cobalt.io/assets" \
  -H "Accept: application/vnd.cobalt.v1+json" \
  -H "Authorization: Bearer YOUR-PERSONAL-API-TOKEN" \
  -H "X-Org-Token: YOUR-V1-ORGANIZATION-TOKEN"
```

> Response Sample

```json
{
  "data": [
    {
      "resource": {
        "id": "as_rvZRC5Y",
        "title": "Acme Corp. HR System",
        "description": "HR system of the Acme Corp. holding sensitive employee data",
        "asset_type": "web",
        "logo": "https://s3.amazonaws.com/acmecorp/uploads/attachment/file/12345/cat.jpeg?something=1",
        "attachments": [
          {
            "token": "att_yYXZodA",
            "download_url": "https://s3.amazonaws.com/acmecorp/uploads/attachment/file/12345/rainbow.jpeg?something=1"
          }
        ]
      },
      "links": {
        "ui": {
          "url": "https://api.cobalt.io/links/eyJ0eXBlIjoic29tZXRoaW5nIiwib3JnU2x1ZyI6ImNvYmFsdCIsInBlbnRlc3RUYWciOiJz="
        }
      }
    }
  ],
  "pagination": {
    "next_page": "/assets?cursor=a1b2c3d4",
    "prev_page": "/assets?cursor=4d3c2b1a"
  }
}
```

Returns all assets that belong to an organization.

{{% add-org-token %}}

### HTTP Request

`GET https://api.cobalt.io/assets`

### Query Parameters

| Name | Default | Description                                                                                                 |
|-----------|---------|-------------------------------------------------------------------------------------------------------------|
| `cursor`  | N/A     | {{% cursor %}} Example: `https://api.cobalt.io/assets?cursor=a1b2c3d4`            |
| `limit`   | `10`    | {{% limit %}} Example: `https://api.cobalt.io/assets?limit=5` |

### Response Parameters

| Name          | Description                                                                                                                               |
|----------------|-------------------------------------------------------------------------------------------------------------------------------------------|
| `id`           | {{% asset-id %}} |
| `title`        | {{% asset-title %}} |
| `description`  | {{% asset-description %}} |
| `asset_type`   | {{% asset-type %}} |
| `links.ui.url` | {{% links-ui-url %}} |
| `logo`         | {{% asset-logo %}} |
| `attachments`  | {{% asset-attachments %}} |

### Asset Types

{{% asset-types-list %}}
