---
weight: 11
title: Webhooks
---

# Webhooks

Webhooks allow your system to be notified when events occur on the Cobalt Platform via HTTP POST requests.
This eliminates the need to poll the API for updates.

## Get all webhooks

```sh
curl -X GET "https://api.cobalt.io/webhooks" \
  -H "Accept: application/vnd.cobalt.v2+json" \
  -H "Authorization: Bearer YOUR-PERSONAL-API-TOKEN" \
  -H "X-Org-Token: YOUR-V2-ORGANIZATION-TOKEN"
```

> The above command returns JSON structured like this:

```json
{
  "pagination": {
    "next_page": null,
    "prev_page": null
  },
  "data": [
    {
      "resource": {
        "id": "wb_38URp3gxZqfkjEXmkybrrs",
        "name": "My Webhook",
        "url": "https://example.local",
        "active": true,
        "unhealthy_since": null,
        "user": "us_RxvqT5T3WCFrfTF74B6JLC"
      }
    }
  ]
}
```

This endpoint retrieves a list of all webhooks that belong to your organization.

### HTTP Request

`GET https://api.cobalt.io/webhooks`

### URL Parameters

| Parameter | Default | Description                                                                                              |
|-----------|---------|----------------------------------------------------------------------------------------------------------|
| `cursor`  | N/A     | Used for [pagination](./#pagination), e.g. `https://api.cobalt.io/webhooks?cursor=a1b2c3d4`              |
| `limit`   | `10`    | If specified, returns only a specified amount of webhooks, e.g. `https://api.cobalt.io/webhooks?limit=5` |

### Response Fields

| Field                | Description                                            |
|----------------------|--------------------------------------------------------|
| id                   | The ID of the webhook                                  |
| name                 | The name of the webhook                                |
| url                  | The URL that webhook events are sent to                |
| active               | A boolean flag that indicates if the webhook is active |
| unhealthy_since      | The time that we began failing to deliver events to this webhook. If the webhook is unhealthy, this field will contain an ISO8601 time stamp. Ex: `2022-08-30T14:14:14.000Z`    |
| user                 | The ID of the user that created the webhook            |

## Get a webhook

```sh
curl -X GET "https://api.cobalt.io/webhooks/YOUR-WEBHOOK-IDENTIFIER" \
  -H "Accept: application/vnd.cobalt.v2+json" \
  -H "Authorization: Bearer YOUR-PERSONAL-API-TOKEN" \
  -H "X-Org-Token: YOUR-V2-ORGANIZATION-TOKEN"
```

> The above command returns JSON structured like this:

```json
{
  "resource": {
    "id": "wb_38URp3gxZqfkjEXmkybrrs",
    "name": "My Webhook",
    "url": "https://example.local",
    "active": true,
    "unhealthy_since": null,
    "user": "us_RxvqT5T3WCFrfTF74B6JLC"
  }
}
```

This endpoint retrieves a specific webhook belonging to your organization.

### HTTP Request

`GET https://api.cobalt.io/webhooks/YOUR-WEBHOOK-IDENTIFIER`

### Response Fields

| Field                | Description                                                         |
|----------------------|---------------------------------------------------------------------|
| id                   | The ID of the webhook                                               |
| name                 | The name of the webhook                                             |
| url                  | The URL that webhook events are sent to                             |
| active               | A boolean flag that indicates if the webhook is active              |
| unhealthy_since      | The time that we began failing to deliver events to this webhook. If the webhook is unhealthy, this field will contain an ISO8601 time stamp. Ex: `2022-08-30T14:14:14.000Z`    |
| user                 | The ID of the user that created the webhook                         |

<aside class="notice">
Remember - you can only request a webhook scoped to the organization specified in the <code>X-Org-Token</code> header.
</aside>

## Create a webhook

```sh
curl -X POST "https://api.cobalt.io/webhooks" \
  -H 'Accept: application/vnd.cobalt.v2+json' \
  -H 'Authorization: Bearer YOUR-PERSONAL-API-TOKEN' \
  -H 'Content-Type: application/vnd.cobalt.v2+json' \
  -H 'Idempotency-Key: A-UNIQUE-IDENTIFIER-TO-PREVENT-UNINTENTIONAL-DUPLICATION' \
  -H 'X-Org-Token: YOUR-V2-ORGANIZATION-TOKEN' \
  --data '{
            "name": "My Webhook",
            "active": true,
            "authentication_token": "my_secret_token",
            "url": "https://example.local/webhook"
          }'
```

> The above command returns no data and a `201` response code when successful. There will be a `Location` header
> pointing at the newly-created webhook.

This endpoint creates a new webhook belonging to your organization.

When you attempt to create a webhook, we will send a test event to your endpoint to validate that events
can be delivered successfully. Your endpoint must respond with the HTTP 204 status code. For details on
test events, see the [Webhook Events](./#webhook-events) section below.

### HTTP Request

`POST https://api.cobalt.io/webhooks`

### Body

| Field                | Description                                              |
|----------------------|----------------------------------------------------------|
| name                 | The name of the webhook                                  |
| active               | A boolean flag specifying if the webhook is active       |
| authentication_token | An arbitrary string value. We include this value in the `X-Authentication-Token` header when we send webhook events to you. You can use this to verify that the events you receive are really from Cobalt. |
| url                  | The URL to send events to                                |

### Response

On successful creation, a `201` response code will be returned. A response header, `Location`, will contain the URL
within Cobalt's API of the new webhook.

<aside class="notice">
Multiple webhooks may not have the same name or URL within an organization.
</aside>

<aside class="notice">
Remember - you can only create a webhook within the organization specified in the <code>X-Org-Token</code> header.
</aside>

## Update a webhook

```sh
curl -X PATCH 'https://api.cobalt.io/webhooks/YOUR-WEBHOOK-IDENTIFIER' \
  -H 'Accept: application/vnd.cobalt.v2+json' \
  -H 'Authorization: Bearer YOUR-PERSONAL-API-TOKEN' \
  -H 'Content-Type: application/vnd.cobalt.v2+json' \
  -H 'X-Org-Token: YOUR-V2-ORGANIZATION-TOKEN' \
  --data '{
            "name": "FooBar",
            "authentication_token": "super_secret_token",
            "active": false,
            "url": "https://example.local/webhook2"
          }'
```

> The above command returns no data and a `204` response code when successful.

This endpoint updates a webhook belonging to your organization.

### HTTP Request

`PATCH https://api.cobalt.io/webhooks/YOUR-WEBHOOK-IDENTIFIER`

### Body

All body fields are optional. You only need to include the fields that should be updated.

| Field                | Description                                        |
|----------------------|----------------------------------------------------|
| name                 | The name of the webhook                            |
| authentication_token | An arbitrary string value. We include this value in the `X-Authentication-Token` header when we send webhook events to you. You can use this to verify that the events you receive are really from Cobalt. |
| active               | A boolean flag specifying if the webhook is active |
| url                  | The URL to send events to                          |

### Response

On a successful update, a `204` response code will be returned.

<aside class="notice">
Multiple webhooks may not have the same name or URL within an organization.
</aside>

<aside class="notice">
Remember - you can only update a webhook within the organization specified in the <code>X-Org-Token</code> header.
</aside>

## Delete a webhook

```sh
curl -X DELETE 'https://api.cobalt.io/webhooks/YOUR-WEBHOOK-IDENTIFIER' \
  -H 'Accept: application/vnd.cobalt.v2+json' \
  -H 'Authorization: Bearer YOUR-PERSONAL-API-TOKEN' \
  -H 'Content-Type: application/vnd.cobalt.v2+json' \
  -H 'X-Org-Token: YOUR-V2-ORGANIZATION-TOKEN'
```

> The above command returns no data and a `204` response code when successful.

This endpoint deletes a webhook belonging to your organization.

### HTTP Request

`DELETE https://api.cobalt.io/webhooks/YOUR-WEBHOOK-IDENTIFIER`

### Response

On successful deletion, a `204` response code will be returned.

<aside class="notice">
Remember - you can only delete a webhook within the organization specified in the <code>X-Org-Token</code> header.
</aside>

## Webhook Events

Webhook event properties:

| Field         | Description                                |
|---------------|--------------------------------------------|
| id            | The ID of the webhook event                |
| action        | The action that the event is related to    |
| subject       | The subject that the event is related to   |
| timestamp     | The time that the event ocurred            |

`action` types:

* `TEST_EVENT`
* `PENTEST_CREATED`
* `FINDING_PUBLISHED`
* `FINDING_STATE_UPDATED`

`subject` properties:

| Field         | Description                                |
|---------------|--------------------------------------------|
| id            | The ID of the subject resource             |
| type          | The type of the subject resource           |

`subject` types:

* `TEST_EVENT`
* `PENTEST`
* `FINDING`

```json
{
  "id": "eve_4tvptSU2SyqupRGQ4Jawdx",
  "action": "PENTEST_CREATED",
  "subject": {
    "id": "eve_4tvptSU2SyqupRGQ4Jawdx",
    "type": "PENTEST"
  },
  "timestamp": "2022-09-17T17:14:06.734Z"
}
```

## Webhook Delivery and Health

Delivery process:

* An event occurs on the Cobalt Platform that you are subscribed to
* Cobalt will attempt to send the event to your webhook endpoint via an HTTP POST
request. If your endpoint responds with an HTTP `204` status then we will mark the
delivery as successful.
* If your endpoint does not respond with an HTTP `204` status then we will attempt
to send the event 5 more times with 5 seconds between each request.
* If none of the delivery attempt succeed, then we will mark your webhook endpoint
as unhealthy and put the event into our failed events queue.
* On an hourly interval we will attempt to redeliver failed events.
* If your webhook endpoint becomes able to receive events again, we will mark your
webhook endpoint as healthy.
* If your webhook endpoint stays unhealthy for 48 hours then we will deactivate your webhook.

If your webhook becomes deactivated then you will need to activate it again via the API.

## Best Practices

1. Set your webhook authentication token to a high-entrophy value of sufficient length.
When you receive an event, check that the value in the `X-Authentication-Token` header
matches your authentication token. This ensures that you do not process fraudulent
webhook events from a threat actor.
2. Don't add expensive operations to the endpoint that receives webhook events.
A common pattern is to receive webhook events with a lightweight endpoint that
publishes received events to a message queue that can be processed by your components
containing business logic. This keeps the latency and failure rate of your webhook
endpoint low.
