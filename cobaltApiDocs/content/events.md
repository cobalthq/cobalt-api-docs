---
weight: 15
title: Events
---

# Events

## Get All Events

```shell
curl -X GET "https://api.cobalt.io/events" 
  -H "accept: application/vnd.cobalt.v1+json" 
  -H "Authorization: Bearer your-personal-api-token-here" 
  -H "X-Org-Token: your-org-token-here"

```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "resource": {
        "id": "WIP"
      }
    }
 ]
}
```

This endpoint retrieves a list of all events happening across the organization specified in the header.


### HTTP Request

`GET https://api.cobalt.io/events`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
limit | 100 | If set, you can adjust the limit returned, e.g. https://api.cobalt.io/events?limit=1000

<aside class="success">
Remember — you can only request Pentests scoped to the Org specified in the header.
</aside>
