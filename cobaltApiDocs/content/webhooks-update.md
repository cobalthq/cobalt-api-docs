---
weight: 21
title: Update Webhook
---

## Update Webhook


```shell
curl -X PATCH "https://api.cobalt.io/webhooks/{webhook-id}" \
  -H "accept: application/vnd.cobalt.v1+json" \
  -H "content-type: application/vnd.cobalt.v1+json" \
  -H "Authorization: Bearer your-personal-api-token-here" \
  -H "Mutation-Check: mutation-check" \
  -H "X-Org-Token: your-org-token-here"
```

<aside class="success">
Of note — the `content-type` header is required for incoming data in POST/PUT/PATCH requests.
</aside>

> The above command accepts JSON structured like this:

```json
{
  "active": true
} 
```

> and returns JSON structured like this:

```json
{
}

```

This endpoint enables you to update a specific webhook. You can specify which webhook by the `id` directly in the request URL.

### HTTP Request

`PATCH https://api.cobalt.io/webhooks/{webhook-id}`

### Fields

Field             | Description
----------------- | -----------
`active`          | Boolean to set the webhook to active or inactive (true|false)
`publisherToken`  | todo
`consumerToken`   | todo

