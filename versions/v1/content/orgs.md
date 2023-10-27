---
weight: 4
title: Organizations
---

# Organizations

## Get All Organizations

```sh
curl -X GET "https://api.us.cobalt.io/orgs" \
  -H "Accept: application/vnd.cobalt.v1+json" \
  -H "Authorization: Bearer YOUR-PERSONAL-API-TOKEN"
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "resource": {
        "id": "or_A2bb4FE",
        "name": "Acme Corp.",
        "token": "e9d6da*********0e8ad"
      },
      "links": {
        "ui": {
          "url": "https://api.us.cobalt.io/links/eyJ0eXBlIjoic29tZXRoaW5nIiwib3JnU2x1ZyI6ImNvYmFsdCIsInBlbnRlc3RUYWciOiJz="
        }
      }
    },
    {
      "resource": {
        "id": "or_UX2Fg3",
        "name": "Lorem Corp.",
        "token": "dfd6da*********0e8ad"
      },
      "links": {
        "ui": {
          "url": "https://api.us.cobalt.io/links/eyJ0eXBlIjoic29tZXRoaW5nIiwib3JnU2x1ZyI6ImNvYmFsdCIsInBlbnRlc3RUYWciOiJz="
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

This endpoint retrieves a list of organizations, or *orgs*, that you belong to. Save the `token` field to be used in
your `X-Org-Token` header in subsequent calls in querying for assets, findings, pentests and events that belong to that
organization.

### HTTP Request

`GET https://api.us.cobalt.io/orgs`

### URL Parameters

| Parameter | Default | Description                                                                                                      |
|-----------|---------|------------------------------------------------------------------------------------------------------------------|
| `cursor`  | N/A     | Used for [pagination](./#pagination). Example: `https://api.us.cobalt.io/orgs?cursor=a1b2c3d4`                   |
| `limit`   | `10`    | If specified, returns only a specified amount of organizations. Example: `https://api.us.cobalt.io/orgs?limit=5` |

### Response Fields

| Field          | Description                                                                              |
|----------------|------------------------------------------------------------------------------------------|
| `id`           | A unique ID representing the organization. Starts with `or_`                             |
| `name`         | The name of the organization                                                             |
| `token`        | The organization token you'll need in subsequent calls                                   |
| `links.ui.url` | A link to redirect an authorized user to this organization in the Cobalt web application |

<aside class="notice">
Remember - Save the <code>token</code> attribute from the response body. You will need it in subsequent calls as the
value of the <code>X-Org-Token</code> header.
</aside>
