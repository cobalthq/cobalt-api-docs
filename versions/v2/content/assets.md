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

> Response Sample

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
            "title": "React 18.0.0"
          }
        ],
        "attachments": [
          {
            "id": "at_LA5GcEL4HRitFGCHREqmzL",
            "file_name": "rainbow.jpeg",
            "download_url": "https://s3.amazonaws.com/acmecorp/uploads/attachment/file/12345/rainbow.jpeg?something=1"
          }
        ],
        "tags": [
          {
            "name": "tag1"
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

| Name             | Default | Description                                                                                                                                                                                                                                                                                   |
|-----------------------|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `cursor`              | N/A     | {{% cursor %}} Example: `https://api.cobalt.io/assets?cursor=a1b2c3d4`                                                                                                                                                                                                 |
| `limit`               | `10`    | {{% limit %}} Example: `https://api.cobalt.io/assets?limit=5`                                                                                                                                                                                      |
| `asset_type`          | N/A     | If specified, returns assets that match `asset_type`. See Response Parameters below for example `asset_type` values. Example: `https://api.cobalt.io/assets?asset_type=web`. Returns an empty list if no assets match the `asset_type` filter.                                                    |
| `tags_contains_all[]` | N/A     | If specified, returns assets that contain all matching `tags`. This query parameter can be specified multiple times. Returns an empty list if no matches are found. Example: `https://api.cobalt.io/assets?tags_contains_all[]=third party&tags_contains_all[]=some-tag-id`                   |
| `sort`                | N/A     | If specified, returns assets sorted by one of the chosen parameters: `asset_type`. When defined, records are returned in ascending order by the sort parameter. To return in descending order, use a `-` before the sort parameter. Example: `https://api.cobalt.io/assets?sort=-asset_type`. |

### Response Parameters

| Name              | Description                                                                                                                                                                                               |
|--------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `id`               | A unique ID representing the asset. Starts with `as_`                                                                                                                                                     |
| `title`            | The title of the asset; set by user creating the asset                                                                                                                                                    |
| `description`      | A description of the asset; set by user creating the asset                                                                                                                                                |
| `asset_type`       | An asset type, such as; `api`, `cloud_config`, `external_network`, `internal_network`, `mobile`, `web`, `web_plus_api`, `web_plus_mobile`, `wireless_network`, `iot`, `thick_client`, `physical`, `other` |
| `logo`             | A link pointing the location of the uploaded asset logo                                                                                                                                                   |
| `technology_stack` | A list of technology stacks. Each element contains the title of the technology. Example: React 18.0.0.                                                                                                    |
| `attachments`      | A list of asset attachments. Attachment download URLs are pre-authorized and will expire after 10 minutes.                                                                                                |
| `tags`             | A list of tags. A tag has a `name` attribute. Example: `[{"name": "third-party system-id"}, {"name": "some-tag-id"}]`                                                                                     |
| `links.ui.url`     | A link to redirect an authorized user to this asset in the Cobalt web application                                                                                                                         |

## Get an Asset

```sh
curl -X GET "https://api.cobalt.io/assets/YOUR-ASSET-IDENTIFIER" \
  -H "Accept: application/vnd.cobalt.v2+json" \
  -H "Authorization: Bearer YOUR-PERSONAL-API-TOKEN" \
  -H "X-Org-Token: YOUR-V2-ORGANIZATION-TOKEN"
```

> Response Sample

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
          "title": "React 18.0.0"
        }
      ],
      "attachments": [
        {
          "id": "at_LA5GcEL4HRitFGCHREqmzL",
          "file_name": "rainbow.jpeg",
          "download_url": "https://s3.amazonaws.com/acmecorp/uploads/attachment/file/12345/rainbow.jpeg?something=1"
        }
      ],
      "tags": [
        {
          "name": "tag1"
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

Returns an asset that belongs to an organization.

{{% add-org-token %}}

### HTTP Request

`GET https://api.cobalt.io/assets/YOUR-ASSET-IDENTIFIER`

### Response Parameters

| Name              | Description                                                                                                                                                                                               |
|--------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `id`               | A unique ID representing the asset. Starts with `as_`                                                                                                                                                     |
| `title`            | The title of the asset; set by user creating the asset                                                                                                                                                    |
| `description`      | A description of the asset; set by user creating the asset                                                                                                                                                |
| `asset_type`       | An asset type, such as; `api`, `cloud_config`, `external_network`, `internal_network`, `mobile`, `web`, `web_plus_api`, `web_plus_mobile`, `wireless_network`, `iot`, `thick_client`, `physical`, `other` |
| `logo`             | A link pointing the location of the uploaded asset logo                                                                                                                                                   |
| `technology_stack` | A list of technology stacks. Each element contains the title of the technology. Example: React 18.0.0.                                                                                                    |
| `attachments`      | A list of asset attachments (including the logo). Attachment download URLs are pre-authorized and will expire after 10 minutes.                                                                           |
| `tags`             | A list of tags. A tag has a `name` attribute. Example: `[{"name": "third-party system-id"}, {"name": "some-tag-id"}]`                                                                                     |
| `links.ui.url`     | A link to redirect an authorized user to this asset in the Cobalt web application                                                                                                                         |

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
            "asset_type": "web",
            "tags": []
          }'
```

> {{% 201-code %}} There will be a `Location` header
> pointing at the newly created asset.

Creates a new asset for an organization.

{{% add-org-token %}}

### HTTP Request

`POST https://api.cobalt.io/assets`

### Request Body

| Name         | Description                                                                                                                                                                          |
|---------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `title`       | The title of the asset; set by user creating the asset                                                                                                                               |
| `description` | Optional; A description of the asset; set by user creating the asset                                                                                                                 |
| `asset_type`  | `api`, `cloud_config`, `external_network`, `internal_network`, `mobile`, `web`, `web_plus_api`, `web_plus_mobile`, `wireless_network`, `iot`, `thick_client`, `physical`, or `other` |
| `tags`        | Optional; A list of tags. A tag has a `name` attribute. Example: `[{"name": "third-party system-id"}, {"name": "some-tag-id"}]`. Defaults to empty list if not provided              |

### Response

{{% 201-code %}} The `Location` response header contains the URL of the new
asset within the Cobalt API.

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
            "asset_type": "web",
            "tags: []
          }'
```

> {{% 204-code %}}

Updates an asset with the provided details.

{{% add-org-token %}}

### HTTP Request

`PUT https://api.cobalt.io/assets/YOUR-ASSET-IDENTIFIER`

### Request Body

| Name         | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `title`       | The title of the asset; set by user creating the asset                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| `description` | Optional; A description of the asset; set by user creating the asset                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `asset_type`  | Options: `api`, `cloud_config`, `external_network`, `internal_network`, `mobile`, `web`, `web_plus_api`, `web_plus_mobile`, `wireless_network`, `iot`, `thick_client`, `physical`, `other`                                                                                                                                                                                                                                                                                                                                                      |
| `tags`        | Optional; A list of tags. A tag has a `name` attribute. Example: `[{"name": "third-party system-id"}, {"name": "some-tag-id"}]`. If `tags` field is not provided in the `PUT` request, no changes will occur to the asset tags. Any `tags` that **already exist for the asset and are not provided** in the `PUT` request will be deleted. Any `tags` **that already exist for the asset and are provided** in the `PUT` request will remain. Any `tags` that do not exist for the asset and are provided in the `PUT` request will be created. |

### Response

{{% 204-code %}}

## Delete an Asset

```sh
curl -X DELETE 'https://api.cobalt.io/assets/YOUR-ASSET-IDENTIFIER' \
  -H 'Accept: application/vnd.cobalt.v2+json' \
  -H 'Authorization: Bearer YOUR-PERSONAL-API-TOKEN' \
  -H 'Content-Type: application/vnd.cobalt.v2+json' \
  -H 'X-Org-Token: YOUR-V2-ORGANIZATION-TOKEN'
```

> {{% 204-code %}}

Deletes an asset that belongs to an organization.
This request also deletes all `tags` associated with the asset.

{{% add-org-token %}}

### HTTP Request

`DELETE https://api.cobalt.io/assets/YOUR-ASSET-IDENTIFIER`

### Response

{{% 204-code %}}

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

> {{% 201-code %}} There will be a `Location` header
> pointing at the newly created attachment.

Adds an attachment to an asset.

{{% add-org-token %}}

### HTTP Request

`POST https://api.cobalt.io/assets/YOUR-ASSET-IDENTIFIER/attachments`

### Request Body

| Form Field   | Description                          |
|--------------|--------------------------------------|
| `attachment` | The file to upload as an attachment. |

### File Requirements

The file must be smaller than 10 MB.

### Response

{{% 201-code %}} A response header, `Location`, will contain the URL within
Cobalt API of the new attachment which you can use only to DELETE the attachment.

## Delete an Attachment

```sh
curl -X DELETE 'https://api.cobalt.io/assets/YOUR-ASSET-IDENTIFIER/attachments/YOUR-ATTACHMENT-IDENTIFIER' \
  -H 'Accept: application/vnd.cobalt.v2+json' \
  -H 'Authorization: Bearer YOUR-PERSONAL-API-TOKEN' \
  -H 'X-Org-Token: YOUR-V2-ORGANIZATION-TOKEN'
```

> {{% 204-code %}}

Deletes an attachment from an asset.

{{% add-org-token %}}

### HTTP Request

`DELETE https://api.cobalt.io/assets/YOUR-ASSET-IDENTIFIER/attachments/YOUR-ATTACHMENT-IDENTIFIER`

> You can obtain this URL from the `Location` response header of the create attachment endpoint, or build it by getting
> the attachment identifier from the response data of the `GET /assets` endpoint.

### Response

{{% 204-code %}}

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

> {{% 201-code %}}

Adds a new logo to an asset. This request removes the old logo and replaces it with a new logo.

{{% add-org-token %}}

### HTTP Request

`POST https://api.cobalt.io/assets/YOUR-ASSET-IDENTIFIER/logo`

### Request Body

| Form Field   | Description                   |
|--------------|-------------------------------|
| `attachment` | The file to upload as a logo. |

### File Requirements

- The file must be an image, for example a `.png` or `.jpg`.
- The file must be smaller than 10 MB.

### Response

{{% 201-code %}}
