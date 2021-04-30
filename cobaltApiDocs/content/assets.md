---
weight: 12
title: Assets
---

# Assets

## Get All Assets

```shell
curl -X GET "https://api.cobalt.io/assets" \
  -H "accept: application/vnd.cobalt.v1+json" \
  -H "Authorization: Bearer your-personal-api-token-here" \
  -H "X-Org-Token: your-org-token-here"
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
      }
    }
 ]
}
```

This endpoint retrieves a list of assets that belong to the org specified in the header.


### HTTP Request

`GET https://api.cobalt.io/assets`

### Fields

Field          | Description
-------------  | -----------
`id`           | The Cobalt id of the asset
`title`        | The title of the asset
`description`  | A description of the asset
`asset_type`   | api, cloud_config, external_network, internal_network, mobile, web, web_plus_api, web_plus_mobile  


<aside class="success">
Remember — you can only request Assets scoped to the Org specified in the header.
</aside>
