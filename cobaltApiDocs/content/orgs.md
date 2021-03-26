---
weight: 11
title: Orgs
---

# Orgs

## Get All Orgs

```shell
curl -X GET "https://api.cobalt.io/orgs" 
  -H "accept: application/vnd.cobalt.v1+json" 
  -H  "Authorization: Bearer your-personal-api-token-here"
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "resource": {
        "id": "1955",
        "name": "Banana",
        "token": "save-this-org-token"
      }
    },
    {
      "resource": {
        "id": "2546",
        "name": "Saxophone - Alto",
        "token": "or-save-this-org-token"
      }
    }
  ]
}
```

This endpoint retrieves a list of organizations, i.e. *orgs*, that you belong to. Save the `token` field to be used as your `X-Org-Token` field in subsequent calls in querying for assets, findings, pentests and events that belong to that org. 


### HTTP Request

`GET https://api.cobalt.io/orgs`


<aside class="success">
Remember — Save that org token for use in subsequent API calls as part of your header.
</aside>
