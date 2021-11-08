---
weight: 18
title: Webhooks
---

# Webhooks

## Get All Webhooks

```shell
curl -X GET "https://api.cobalt.io/webhooks" \
  -H "accept: application/vnd.cobalt.v1+json" \
  -H "Authorization: Bearer your-personal-api-token-here" 
  -H "X-Org-Token: your-org-token-here"
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "resource": {
        "id": "string",
        "url": "https://an-address-to-receive-events",
        "active": true,
        "healthy": true,
        "authentication": {
          "publisherToken": "a-publisher-token-here",
          "consumerToken": "a-consumer-token-here"
        }
      }
    }
  ]
}

```

This endpoint retrieves a list of all tokens that belong to you. 

### HTTP Request

`GET https://api.cobalt.io/webhooks`

### Fields

Field             | Description
----------------- | -----------
`id`              | todo
`url`             | todo
`active`          | todo
`healthy`         | todo
`publisherToken`  | todo
`consumerToken`   | todo

