---
weight: 5
title: Assets
---

# Assets

## Get All Assets

```sh
curl -X GET 'https://api.cobalt.io/assets' \
  -H 'Accept: application/vnd.cobalt.v2+json' \
  -H 'Authorization: Bearer YOUR-PERSONAL-API-TOKEN' \
  -H 'X-Org-Token: YOUR-V2-ORGANIZATION-TOKEN'
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "resource": {
        "id": "an-asset-identifier-here",
        "title": "Azure External Network ",
        "description": "Test text",
        "asset_type": "external_network",
        "attachments": []
      },
      "links": {
        "ui": {
          "url": "https://api.cobalt.io/links/long-web-app-redirect-to-this-asset"
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

This endpoint retrieves a list of assets that belong to the org specified in the header.

### HTTP Request

`GET https://api.cobalt.io/assets`

### URL Parameters

Parameter | Default | Description
--------- | ------- | -----------
cursor | N/A | Used for [pagination](./#pagination), e.g. `https://api.cobalt.io/assets?cursor=a1b2c3d4`
limit | `10` | If specified, returns only `limit` assets, e.g. `https://api.cobalt.io/assets?limit=5`

### Response Fields

| Field         | Description                                                                                       |
|---------------|---------------------------------------------------------------------------------------------------|
| `id`          | The Cobalt id of the asset                                                                        |
| `title`       | The title of the asset; set by user creating the asset                                            |
| `description` | A description of the asset; set by user creating the asset                                        |
| `asset_type`  | api, cloud_config, external_network, internal_network, mobile, web, web_plus_api, web_plus_mobile |
| `attachments` | A list of asset attachments (including the logo)                                                  |
| `url`         | The links.ui.url will redirect an authorized user to this asset in the Cobalt platform            |

<aside class="success">
Remember — you can only request Assets scoped to the Org specified in the header.
</aside>

## Get One Asset

```sh
curl -X GET 'https://api.cobalt.io/assets/your-asset-identifier-here' \
  -H 'Accept: application/vnd.cobalt.v2+json' \
  -H 'Authorization: Bearer YOUR-PERSONAL-API-TOKEN' \
  -H 'X-Org-Token: YOUR-V2-ORGANIZATION-TOKEN'
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "resource": {
      "id": "your-asset-identifier-here",
      "title": "Azure External Network ",
      "description": "Test text",
      "asset_type": "external_network",
      "attachments": []
    },
    "links": {
      "ui": {
        "url": "https://api.cobalt.io/links/long-web-app-redirect-to-this-asset"
      }
    }
  }
}
```

This endpoint retrieves a specific asset belonging to the org specified in the header.

### HTTP Request

`GET https://api.cobalt.io/assets/your-asset-identifier-here`

### Response Fields

| Field         | Description                                                                                       |
|---------------|---------------------------------------------------------------------------------------------------|
| `id`          | The Cobalt id of the asset                                                                        |
| `title`       | The title of the asset; set by user creating the asset                                            |
| `description` | A description of the asset; set by user creating the asset                                        |
| `asset_type`  | api, cloud_config, external_network, internal_network, mobile, web, web_plus_api, web_plus_mobile |
| `attachments` | A list of asset attachments (including the logo)                                                  |
| `url`         | The links.ui.url will redirect an authorized user to this asset in the Cobalt platform            |

<aside class="success">
Remember — you can only request an asset scoped to the Org specified in the header.
</aside>

## Create Asset

```sh
curl -X POST "https://api.cobalt.io/assets" \
  -H 'Accept: application/vnd.cobalt.v2+json' \
  -H 'Authorization: Bearer YOUR-PERSONAL-API-TOKEN' \
  -H 'Content-Type: application/vnd.cobalt.v2+json' \
  -H 'Idempotency-Key: unique-identifier-to-prevent-unintentional-duplication' \
  -H 'X-Org-Token: YOUR-V2-ORGANIZATION-TOKEN' \
  --data '{
            "title": "Test Asset",
            "description": "description",
            "asset_type": "web",
            "size": "m",
            "coverage": "standard"
          }'
```

> The above command returns no data and a `201` response code when successful.  There will be a
> `location` header pointing at the newly-created asset.

This endpoint creates a new asset belonging to the org specified in the header.

### HTTP Request

`POST https://api.cobalt.io/assets`

### Body

| Field         | Description                                                                                       |
|---------------|---------------------------------------------------------------------------------------------------|
| `title`       | The title of the asset; set by user creating the asset                                            |
| `description` | A description of the asset; set by user creating the asset                                        |
| `asset_type`  | api, cloud_config, external_network, internal_network, mobile, web, web_plus_api, web_plus_mobile |
| `size`        | xs, s, m, l, xl                                                                                   |
| `coverage`    | extra_light, light, standard, large, extra_large                                                  |

### Sizes and Coverages

When the `size` is `m` (medium), `l` (large), or `xl` (extra large), `coverage` can be any of the listed options.

When the `size` is `s` (small), `coverage` can *not* be `extra_light`.

When the `size` is `xs` (extra small), `coverage` can *not* be `extra_light` or `light`.

### Response

On successful creation, a `201` response code will be returned.  A response header, `location`, will
contain the URL within Cobalt's API of the new asset.

<aside class="success">
Remember — you can only create an asset within the Org specified in the header.
</aside>

## Update Asset

```sh
curl -X PUT 'https://api.cobalt.io/assets/your-asset-identifier-here' \
  -H 'Accept: application/vnd.cobalt.v2+json' \
  -H 'Authorization: Bearer YOUR-PERSONAL-API-TOKEN' \
  -H 'Content-Type: application/vnd.cobalt.v2+json' \
  -H 'X-Org-Token: YOUR-V2-ORGANIZATION-TOKEN' \
  --data '{
            "title": "Updated Title",
            "description": "Updated description",
            "asset_type": "web",
            "size": "m",
            "coverage": "standard"
          }'
```

> The above command returns no data and a `204` response code when successful.

This endpoint updates an asset belonging to the org specified in the header.

### HTTP Request

`PUT https://api.cobalt.io/assets/your-asset-identifier-here`

### Body

| Field         | Description                                                                                       |
|---------------|---------------------------------------------------------------------------------------------------|
| `title`       | The title of the asset; set by user creating the asset                                            |
| `description` | A description of the asset; set by user creating the asset                                        |
| `asset_type`  | api, cloud_config, external_network, internal_network, mobile, web, web_plus_api, web_plus_mobile |
| `size`        | xs, s, m, l, xl                                                                                   |
| `coverage`    | extra_light, light, standard, large, extra_large                                                  |

### Response

On a successful update, a `204` response code will be returned.

<aside class="success">
Remember — you can only update an asset within the Org specified in the header.
</aside>

## Delete Asset

```sh
curl -X DELETE 'https://api.cobalt.io/assets/your-asset-identifier-here' \
  -H 'Accept: application/vnd.cobalt.v2+json' \
  -H 'Authorization: Bearer YOUR-PERSONAL-API-TOKEN' \
  -H 'Content-Type: application/vnd.cobalt.v2+json' \
  -H 'X-Org-Token: YOUR-V2-ORGANIZATION-TOKEN'
```

> The above command returns no data and a `204` response code when successful.

This endpoint deletes an asset belonging to the org specified in the header.

### HTTP Request

`DELETE https://api.cobalt.io/assets/your-asset-identifier-here`

### Response

On successful deletion, a `204` response code will be returned.

<aside class="success">
Remember — you can only delete an asset within the Org specified in the header.
</aside>
