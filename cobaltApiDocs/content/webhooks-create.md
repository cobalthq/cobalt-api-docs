---
weight: 19
title: Create Webhook
---

## Create Webhook


```shell
curl -X POST "https://api.cobalt.io/webhooks" \
  -H "accept: application/vnd.cobalt.v1+json" \
  -H "content-type: application/vnd.cobalt.v1+json" \
  -H "Authorization: Bearer your-personal-api-token-here" \
  -H "Mutation-Check: mutation-check" \
  -H "X-Org-Token: your-org-token-here" \
```

<aside class="success">
Of note — the `content-type` header is required for incoming data in POST/PUT/PATCH requests.
</aside>

> The above command accepts JSON structured like this:

```json
{
  "url": "https://your-address-to-receive-events",
  "active": true,
  "authentication": {
    "publisherToken": "your-publisher-token-here",
    "consumerToken": "your-consumer-token-here"
  }
}
```

> and returns JSON structured like this:

```json
{
}

```

This endpoint creates a new webhook to receive events. To ensure ownership of the `url` where events will be received, a mutation check is required.

**TODO:** Define how to develop proper mutation checks and how to interact with various tokens

### HTTP Request

`POST https://api.cobalt.io/webhooks`

### Fields

Field             | Description
----------------- | -----------
`mutation_checks` | todo
`publisherToken`  | todo
`consumerToken`   | todo

