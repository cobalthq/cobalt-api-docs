---
weight: 5
title: Assets
---

# Assets

## Get All Assets

```sh
curl -X GET "https://api.cobalt.io/assets" \
  -H "Accept: application/vnd.cobalt.v2+json" \
  -H "Authorization: Bearer YOUR-PERSONAL-API-TOKEN" \
  -H "X-Org-Token: YOUR-V2-ORGANIZATION-TOKEN"
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "resource": {
        "id": "as_GZgcehapJUNh6mjNuqsE4T",
        "title": "Acme Corp. HR System",
        "description": "HR system of the Acme Corp. holding sensitive employee data",
        "asset_type": "web",
        "logo": "https://s3.amazonaws.com/acmecorp/uploads/attachment/file/12345/cat.jpeg?something=1",
        "technology_stack": [
          {
            "cpe_id": 12345,
            "title": "React 18.0.0"
          }
        ],
        "attachments": [
          {
            "id": "at_LA5GcEL4HRitFGCHREqmzL",
            "file_name": "rainbow.jpeg",
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

This endpoint retrieves a list of assets that belong to the organization specified in the `X-Org-Token` header.

### HTTP Request

`GET https://api.cobalt.io/assets`

### URL Parameters

| Parameter    | Default | Description                                                                                                                                                                                                                                |
|--------------|---------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `cursor`     | N/A     | Used for [pagination](./#pagination). Example: `https://api.cobalt.io/assets?cursor=a1b2c3d4`                                                                                                                                              |
| `limit`      | `10`    | If specified, returns only a specified amount of assets. Example: `https://api.cobalt.io/assets?limit=5`                                                                                                                                   |
| `asset_type` | N/A     | If specified, returns assets that match `asset_type`. See Response Fields below for example `asset_type` values. Example: `https://api.cobalt.io/assets?asset_type=web`. Returns an empty list if no assets match the `asset_type` filter. |

### Response Fields

| Field              | Description                                                                                                                                        |
|--------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| `id`               | A unique ID representing the asset. Starts with `as_`                                                                                              |
| `title`            | The title of the asset; set by user creating the asset                                                                                             |
| `description`      | A description of the asset; set by user creating the asset                                                                                         |
| `asset_type`       | An asset type, such as; `api`, `cloud_config`, `external_network`, `internal_network`, `mobile`, `web`, `web_plus_api`, `web_plus_mobile`          |
| `logo`             | A link pointing the location of the uploaded asset logo                                                                                            |
| `technology_stack` | A list of technology stacks. Each element contains the CPE ID designated by the CPE database and a title of the technology. Example: React 18.0.0. |
| `attachments`      | A list of asset attachments. Attachment download URLs are pre-authorized and will expire after 10 minutes.                                         |
| `links.ui.url`     | A link to redirect an authorized user to this asset in the Cobalt web application                                                                  |

<aside class="notice">
Remember - you can only request assets scoped to the organization specified in the <code>X-Org-Token</code> header.
</aside>

## Get an Asset

```sh
curl -X GET "https://api.cobalt.io/assets/YOUR-ASSET-IDENTIFIER" \
  -H "Accept: application/vnd.cobalt.v2+json" \
  -H "Authorization: Bearer YOUR-PERSONAL-API-TOKEN" \
  -H "X-Org-Token: YOUR-V2-ORGANIZATION-TOKEN"
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "resource": {
      "id": "as_GZgcehapJUNh6mjNuqsE4T",
      "title": "Acme Corp. HR System",
      "description": "HR system of the Acme Corp. holding sensitive employee data",
      "asset_type": "web",
      "logo": "https://s3.amazonaws.com/acmecorp/uploads/attachment/file/12345/cat.jpeg?something=1",
      "technology_stack": [
        {
          "cpe_id": 12345,
          "title": "React 18.0.0"
        }
      ],
      "attachments": [
        {
          "id": "at_LA5GcEL4HRitFGCHREqmzL",
          "file_name": "rainbow.jpeg",
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
}
```

This endpoint retrieves a specific asset belonging to the organization specified in the `X-Org-Token` header.

### HTTP Request

`GET https://api.cobalt.io/assets/YOUR-ASSET-IDENTIFIER`

### Response Fields

| Field              | Description                                                                                                                                        |
|--------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| `id`               | A unique ID representing the asset. Starts with `as_`                                                                                              |
| `title`            | The title of the asset; set by user creating the asset                                                                                             |
| `description`      | A description of the asset; set by user creating the asset                                                                                         |
| `asset_type`       | An asset type, such as; `api`, `cloud_config`, `external_network`, `internal_network`, `mobile`, `web`, `web_plus_api`, `web_plus_mobile`          |
| `logo`             | A link pointing the location of the uploaded asset logo                                                                                            |
| `technology_stack` | A list of technology stacks. Each element contains the CPE ID designated by the CPE database and a title of the technology. Example: React 18.0.0. |
| `attachments`      | A list of asset attachments (including the logo). Attachment download URLs are pre-authorized and will expire after 10 minutes.                    |
| `links.ui.url`     | A link to redirect an authorized user to this asset in the Cobalt web application                                                                  |

<aside class="notice">
Remember - you can only request an asset scoped to the organization specified in the <code>X-Org-Token</code> header.
</aside>

## Create an Asset

```sh
curl -X POST "https://api.cobalt.io/assets" \
  -H 'Accept: application/vnd.cobalt.v2+json' \
  -H 'Authorization: Bearer YOUR-PERSONAL-API-TOKEN' \
  -H 'Content-Type: application/vnd.cobalt.v2+json' \
  -H 'Idempotency-Key: A-UNIQUE-IDENTIFIER-TO-PREVENT-UNINTENTIONAL-DUPLICATION' \
  -H 'X-Org-Token: YOUR-V2-ORGANIZATION-TOKEN' \
  --data '{
            "title": "Test Asset",
            "description": "Lorem ipsum",
            "asset_type": "web"
          }'
```

> The above command returns no data and a `201` response code when successful. There will be a `Location` header
> pointing at the newly created asset.

This endpoint creates a new asset belonging to the organization specified in the `X-Org-Token` header.

### HTTP Request

`POST https://api.cobalt.io/assets`

### Body

| Field         | Description                                                                                                          |
|---------------|----------------------------------------------------------------------------------------------------------------------|
| `title`       | The title of the asset; set by user creating the asset                                                               |
| `description` | Optional; A description of the asset; set by user creating the asset                                                 |
| `asset_type`  | `api`, `cloud_config`, `external_network`, `internal_network`, `mobile`, `web`, `web_plus_api`, or `web_plus_mobile` |

### Response

You get a `201` response code for a successful request. The `Location` response header contains the URL of the new
asset within the Cobalt API.

<aside class="notice">
Remember - you can only create an asset within the organization specified in the <code>X-Org-Token</code> header.
</aside>

## Update an Asset

```sh
curl -X PUT 'https://api.cobalt.io/assets/AN-ASSET-IDENTIFIER' \
  -H 'Accept: application/vnd.cobalt.v2+json' \
  -H 'Authorization: Bearer YOUR-PERSONAL-API-TOKEN' \
  -H 'Content-Type: application/vnd.cobalt.v2+json' \
  -H 'X-Org-Token: YOUR-V2-ORGANIZATION-TOKEN' \
  --data '{
            "title": "Updated title",
            "description": "Updated description",
            "asset_type": "web"
          }'
```

> The above command returns no data and a `204` response code when successful.

This endpoint updates an asset belonging to the organization specified in the `X-Org-Token` header.

### HTTP Request

`PUT https://api.cobalt.io/assets/YOUR-ASSET-IDENTIFIER`

### Body

| Field         | Description                                                                                                                |
|---------------|----------------------------------------------------------------------------------------------------------------------------|
| `title`       | The title of the asset; set by user creating the asset                                                                     |
| `description` | Optional; A description of the asset; set by user creating the asset                                                       |
| `asset_type`  | Options: `api`, `cloud_config`, `external_network`, `internal_network`, `mobile`, `web`, `web_plus_api`, `web_plus_mobile` |

### Response

On a successful update, a `204` response code will be returned.

<aside class="notice">
Remember - you can only update an asset within the organization specified in the <code>X-Org-Token</code> header.
</aside>

## Delete an Asset

```sh
curl -X DELETE 'https://api.cobalt.io/assets/YOUR-ASSET-IDENTIFIER' \
  -H 'Accept: application/vnd.cobalt.v2+json' \
  -H 'Authorization: Bearer YOUR-PERSONAL-API-TOKEN' \
  -H 'Content-Type: application/vnd.cobalt.v2+json' \
  -H 'X-Org-Token: YOUR-V2-ORGANIZATION-TOKEN'
```

> The above command returns no data and a `204` response code when successful.

This endpoint deletes an asset belonging to the organization specified in the header.

### HTTP Request

`DELETE https://api.cobalt.io/assets/YOUR-ASSET-IDENTIFIER`

### Response

On successful deletion, a `204` response code will be returned.

<aside class="notice">
Remember - you can only delete an asset within the organization specified in the <code>X-Org-Token</code> header.
</aside>

## Upload an Attachment

```sh
curl -X POST 'https://api.cobalt.io/assets/YOUR-ASSET-IDENTIFIER/attachments' \
  -H 'Accept: application/vnd.cobalt.v2+json' \
  -H 'Authorization: Bearer YOUR-PERSONAL-API-TOKEN' \
  -H 'Content-Type: multipart/form-data' \
  -H 'Idempotency-Key: A-UNIQUE-IDENTIFIER-TO-PREVENT-UNINTENTIONAL-DUPLICATION' \
  -H 'X-Org-Token: YOUR-V2-ORGANIZATION-TOKEN'
  --form 'attachment=@"/path/to/image.jpg"'
```

> The above command returns no data and a `201` response code when successful. There will be a `Location` header
> pointing at the newly created attachment.

This endpoint uploads a new attachment for an asset belonging to the organization specified in the `X-Org-Token` header.

### HTTP Request

`POST https://api.cobalt.io/assets/YOUR-ASSET-IDENTIFIER/attachments`

### Body

| Form field   | Description                          |
|--------------|--------------------------------------|
| `attachment` | The file to upload as an attachment. |

### File Requirements

- The file must be smaller than 10 MB.

### Response

On successful upload, a `201` response code will be returned. A response header, `Location`, will contain the URL within
Cobalt API of the new attachment which you can use only to DELETE the attachment.

<aside class="notice">
Remember - you can only upload an attachment for an asset within the organization specified in the
<code>X-Org-Token</code> header.
</aside>

## Delete an Attachment

```sh
curl -X DELETE 'https://api.cobalt.io/assets/YOUR-ASSET-IDENTIFIER/attachments/YOUR-ATTACHMENT-IDENTIFIER' \
  -H 'Accept: application/vnd.cobalt.v2+json' \
  -H 'Authorization: Bearer YOUR-PERSONAL-API-TOKEN' \
  -H 'X-Org-Token: YOUR-V2-ORGANIZATION-TOKEN'
```

> The above command returns no data and a `204` response code when successful.

This endpoint deletes an attachment from an asset belonging to the organization specified in the header.

### HTTP Request

`DELETE https://api.cobalt.io/assets/YOUR-ASSET-IDENTIFIER/attachments/YOUR-ATTACHMENT-IDENTIFIER`

> You can obtain this URL from the `Location` response header of the create attachment endpoint, or build it by getting
> the attachment identifier from the response data of the `GET /assets` endpoint.

### Response

On successful deletion, a `204` response code will be returned.

<aside class="notice">
Remember - you can only delete an attachment from an asset within the organization specified in the
<code>X-Org-Token</code> header.
</aside>

## Upload a Logo

```sh
curl -X POST 'https://api.cobalt.io/assets/YOUR-ASSET-IDENTIFIER/logo' \
  -H 'Accept: application/vnd.cobalt.v2+json' \
  -H 'Authorization: Bearer YOUR-PERSONAL-API-TOKEN' \
  -H 'Content-Type: multipart/form-data' \
  -H 'Idempotency-Key: A-UNIQUE-IDENTIFIER-TO-PREVENT-UNINTENTIONAL-UPLOADS' \
  -H 'X-Org-Token: YOUR-V2-ORGANIZATION-TOKEN'
  --form 'attachment=@"/path/to/image.jpg"'
```

> The above command returns no data and a `201` response code when successful.

This endpoint updates the logo for an asset belonging to the organization specified in the `X-Org-Token` header. This
means the old logo is removed and replaced by the new logo.

### HTTP Request

`POST https://api.cobalt.io/assets/YOUR-ASSET-IDENTIFIER/logo`

### Body

| Form field   | Description                   |
|--------------|-------------------------------|
| `attachment` | The file to upload as a logo. |

### File Requirements

- The file must be an image, for example a `.png` or `.jpg`.
- The file must be smaller than 10 MB.

### Response

On successful upload, a `201` response code will be returned.

<aside class="notice">
Remember - you can only upload a logo for an asset within the organization specified in the <code>X-Org-Token</code>
header.
</aside>
