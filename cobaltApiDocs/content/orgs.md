---
weight: 11
title: Orgs
---

# Orgs

## Get All Orgs

```shell
curl -X GET "https://api.cobalt.io/orgs" \
  -H "accept: application/vnd.cobalt.v1+json" \
  -H "Authorization: Bearer your-personal-api-token-here"
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "resource": {
        "id": "1955",
        "name": "Acme Co",
        "token": "save-this-org-token"
      },
      "links": {
        "ui": {
          "url": "https://api.cobalt.io/links/long-web-app-redirect-to-acme-org"
        }
      }
    },
    {
      "resource": {
        "id": "2546",
        "name": "E Corp",
        "token": "or-save-this-org-token"
      },
      "links": {
        "ui": {
          "url": "https://api.cobalt.io/links/long-web-app-redirect-to-e-corp-org"
        }
      }
    }
  ]
}
```

This endpoint retrieves a list of organizations, i.e. *orgs*, that you belong to. Save the `token` field to be used in your `X-Org-Token` header in subsequent calls in querying for assets, findings, pentests and events that belong to that org. 


### HTTP Request

`GET https://api.cobalt.io/orgs`

### Fields

Field       | Description
----------- | -----------
`id`        | The Cobalt id of the org
`name`      | The name of the org
`token`     | The org token you'll need in subsequent calls
`url`       | The links.ui.url will redirect an authorized user to this org in the Cobalt platform


<aside class="success">
Remember — Save that org token for use in subsequent API calls as part of your header.
</aside>
