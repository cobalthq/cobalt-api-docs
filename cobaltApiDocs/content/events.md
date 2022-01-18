---
weight: 15
title: Events
---

# Events

## Get All Events

```shell
curl -X GET "https://api.cobalt.io/events" \
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
        "id": "277603",
        "action": "comment_created",
        "subject": {
          "id": "277603",
          "type": "comment"
        }
      }
    },
    {
      "resource": {
        "id": "277600",
        "action": "pentest_deleted",
        "subject": {
          "id": "277600",
          "type": "program"
        }
      }
    },
    {
      "resource": {
        "id": "277567",
        "action": "finding_created",
        "subject": {
          "id": "277567",
          "type": "vulnerability"
        }
      }
    }
 ]
}
```

This endpoint retrieves a list of all events happening across the org specified in the header. 


### HTTP Request

`GET https://api.cobalt.io/events`


### URL Parameters

Parameter | Default | Description
--------- | ------- | -----------
cursor | n/a | Used for [pagination](#pagination), e.g. `https://api.cobalt.io/events?cursor=123asdzxc`
limit | `1000` | If specified, returns only `limit` events, e.g. `https://api.cobalt.io/events?limit=5`


<aside class="success">
Remember — you can only request Events scoped to the Org specified in the header.
</aside>
