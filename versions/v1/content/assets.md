---
weight: 4
title: Assets
---

# Assets

## Get All Assets

```sh
curl -X GET "https://api.cobalt.io/assets" \
  -H "X-Org-Token: your-org-token-here"
  -H "Accept: application/vnd.cobalt.v1+json" \
  -H "Authorization: Bearer YOUR-PERSONAL-API-TOKEN" \
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "resource": {
        "id": "as_rvZRC5Y",
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
    "next_page": "/assets?cursor=123asdzxc",
    "prev_page": "/assets?cursor=123asdzxd"
  }
}
```

This endpoint retrieves a list of assets that belong to the org specified in the header.

### HTTP Request

`GET https://api.cobalt.io/assets`

### URL Parameters

Parameter | Default | Description
--------- | ------- | -----------
cursor | N/A | Used for [pagination](./#pagination), e.g. `https://api.cobalt.io/assets?cursor=123asdzxc`
limit | `10` | If specified, returns only `limit` assets, e.g. `https://api.cobalt.io/assets?limit=5`

### Response Fields

| Field         | Description                                                                                       |
|---------------|---------------------------------------------------------------------------------------------------|
| `id`          | The Cobalt id of the asset                                                                        |
| `title`       | The title of the asset; set by user creating the asset                                            |
| `description` | A description of the asset; set by user creating the asset                                        |
| `asset_type`  | api, cloud_config, external_network, internal_network, mobile, web, web_plus_api, web_plus_mobile |
| `url`         | The links.ui.url will redirect an authorized user to this asset in the Cobalt platform            |

<aside class="success">
Remember — you can only request Assets scoped to the Org specified in the header.
</aside>
