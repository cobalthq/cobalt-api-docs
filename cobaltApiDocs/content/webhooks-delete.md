---
weight: 22
title: Delete Webhook
---

## Delete Webhook


```shell
curl -X DELETE "https://api.cobalt.io/webhooks/{webhook-id]" \
  -H "accept: application/vnd.cobalt.v1+json" \
  -H "Authorization: Bearer your-personal-api-token-here" \
  -H "X-Org-Token: your-org-token-here"
```

> The above command does not require a JSON body/payload and returns JSON structured like this:

```json
{
}

```

This endpoint enables you to delete a specific webhook. Place the webhook `id` directly in the request URL. 

### HTTP Request

`DELETE https://api.cobalt.io/webhooks/{webhook-id]`



