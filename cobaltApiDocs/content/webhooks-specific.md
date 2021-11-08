---
weight: 20
title: Get Specific Webhook
---

## Get Specific Webhook


```shell
curl -X GET "https://api.cobalt.io/webhooks/{webhook-id}" \
  -H "accept: application/vnd.cobalt.v1+json" \
  -H "Authorization: Bearer your-personal-api-token-here" \
  -H "Mutation-Check: mutation-check" \
  -H "X-Org-Token: your-org-token-here"
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "resource": {
        "id": "todo",
        "todo": "todo",
        "todo": null
      }
    }
 ]
}

```

This endpoint retrieves a specific webhook. You can specify which webhook by the `id` directly in the request URL.

### HTTP Request

`GET https://api.cobalt.io/webhooks/{webhook-id}`

### Fields

Field             | Description
----------------- | -----------
`mutation_checks` | todo
`publisherToken`  | todo
`consumerToken`   | todo

