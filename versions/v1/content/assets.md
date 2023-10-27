---
weight: 5
title: Assets
---

# Assets

## Get All Assets

```sh
curl -X GET "https://api.us.cobalt.io/assets" \
  -H "Accept: application/vnd.cobalt.v1+json" \
  -H "Authorization: Bearer YOUR-PERSONAL-API-TOKEN" \
  -H "X-Org-Token: YOUR-V1-ORGANIZATION-TOKEN"
```

> This command returns JSON structured like this:

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
          "url": "https://api.us.cobalt.io/links/eyJ0eXBlIjoic29tZXRoaW5nIiwib3JnU2x1ZyI6ImNvYmFsdCIsInBlbnRlc3RUYWciOiJz="
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

This endpoint retrieves a list of assets that belong to the organization specified in the `X-Org-Token` header.

### HTTP Request

`GET https://api.us.cobalt.io/assets`

### URL Parameters

| Parameter | Default | Description                                                                                                 |
|-----------|---------|-------------------------------------------------------------------------------------------------------------|
| `cursor`  | N/A     | Used for [pagination](./#pagination). Example: `https://api.us.cobalt.io/assets?cursor=a1b2c3d4`            |
| `limit`   | `10`    | If specified, returns only a specified amount of assets. Example: `https://api.us.cobalt.io/assets?limit=5` |

### Response Fields

| Field          | Description                                                                                                                               |
|----------------|-------------------------------------------------------------------------------------------------------------------------------------------|
| `id`           | A unique ID representing the asset. Starts with `as_`                                                                                     |
| `title`        | The title of the asset; set by user creating the asset                                                                                    |
| `description`  | A description of the asset; set by user creating the asset                                                                                |
| `asset_type`   | An asset type, such as; `api`, `cloud_config`, `external_network`, `internal_network`, `mobile`, `web`, `web_plus_api`, `web_plus_mobile` |
| `links.ui.url` | A link to redirect an authorized user to this asset in the Cobalt web application                                                         |
| `logo`         | A link pointing the location of the uploaded asset logo                                                                                   |
| `attachments`  | A list of asset attachments. Attachment download URLs are pre-authorized and will expire after 10 minutes.                                |

<aside class="notice">
Remember - you can only request assets scoped to the organization specified in the <code>X-Org-Token</code> header.
</aside>
