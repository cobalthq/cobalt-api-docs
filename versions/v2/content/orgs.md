---
weight: 4
title: Orgs
---

# Organizations

## Get All Organizations

```sh
curl -X GET "https://api.cobalt.io/orgs" \
  -H "accept: application/vnd.cobalt.v2+json" \
  -H "Authorization: Bearer your-personal-api-token-here"
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "resource": {
        "id": "or_Uevoq7MyoYsPT9NPc3conL",
        "name": "Acme Co",
        "token": "save-this-v2-org-token"
      },
      "links": {
        "ui": {
          "url": "https://api.cobalt.io/links/long-web-app-redirect-to-acme-org"
        }
      }
    },
    {
      "resource": {
        "id": "or_SnUYXDBYd2qbaDSuNRNa5q",
        "name": "E Corp",
        "token": "or-save-this-v2-org-token"
      },
      "links": {
        "ui": {
          "url": "https://api.cobalt.io/links/long-web-app-redirect-to-e-corp-org"
        }
      }
    }
  ],
  "pagination": {
    "next_page": "/orgs?cursor=123asdzxc",
    "prev_page": "/orgs?cursor=123asdzxd"
  }
}
```

This endpoint retrieves a list of organizations, i.e. *orgs*, that you belong to. Save the `token` field to be used in
your `X-Org-Token` header in subsequent calls in querying for assets, findings, pentests and events that belong to that
org.

### HTTP Request

`GET https://api.cobalt.io/orgs`

### URL Parameters

| Parameter | Default | Description                                                                              |
|-----------|---------|------------------------------------------------------------------------------------------|
| cursor    | N/A     | Used for [pagination](./#pagination), e.g. `https://api.cobalt.io/orgs?cursor=123asdzxc` |
| limit     | `10`    | If specified, returns only `limit` orgs, e.g. `https://api.cobalt.io/orgs?limit=5`       |

### Response Fields

| Field   | Description                                                                          |
|---------|--------------------------------------------------------------------------------------|
| `id`    | The Cobalt id of the org, an alphanumeric string                                     |
| `name`  | The name of the org                                                                  |
| `token` | The org token you'll need in subsequent calls                                        |
| `url`   | The links.ui.url will redirect an authorized user to this org in the Cobalt platform |

<aside class="success">
Remember — Save that org token for use in subsequent API calls as part of your header.
</aside>