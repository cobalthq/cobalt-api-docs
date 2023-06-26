---
weight: 10
title: Webhooks
---

# Webhooks

Webhooks allow you to send real-time notifications to your system when specific events occur on the Cobalt platform.
We send updates to your URL through HTTP POST requests. This eliminates the need to poll the API for updates.

You can also configure webhooks in the Cobalt web app. <a href="https://developer.cobalt.io/integrations/webhooks/" target="_blank">Learn more</a>.

## Get All Webhooks

```sh
curl -X GET "https://api.cobalt.io/webhooks" \
  -H "Accept: application/vnd.cobalt.v2+json" \
  -H "Authorization: Bearer YOUR-PERSONAL-API-TOKEN" \
  -H "X-Org-Token: YOUR-V2-ORGANIZATION-TOKEN"
```

> Response Sample

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
        "user": "us_RxvqT5T3WCFrfTF74B6JLC",
        "subscribed_event_types": [
          "PENTEST_CREATED",
          "PENTEST_STATE_UPDATED",
          "FINDING_DELETED",
          "FINDING_PUBLISHED",
          "FINDING_STATE_UPDATED",
          "FINDING_UPDATED"
        ]
      }
    }
  ]
}
```

Returns a list of all webhooks that belong to an organization.

{{% add-org-token %}}

### HTTP Request

`GET https://api.cobalt.io/webhooks`

### Query Parameters

| Name | Default | Description                                                                                                     |
|-----------|---------|-----------------------------------------------------------------------------------------------------------------|
| `cursor`  | N/A     | {{% cursor %}} Example: `https://api.cobalt.io/webhooks?cursor=a1b2c3d4`              |
| `limit`   | `10`    | {{% limit %}} Example: `https://api.cobalt.io/webhooks?limit=5` |

### Response Parameters

| Name                  | Description                                                                                                                                                                  |
|------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `id`                     | The ID of the webhook                                                                                                                                                        |
| `name`                   | The name of the webhook                                                                                                                                                      |
| `url`                    | The URL that webhook events are sent to                                                                                                                                      |
| `active`                 | A boolean flag that indicates if the webhook is active                                                                                                                       |
| `unhealthy_since`        | The time that we began failing to deliver events to this webhook. If the webhook is unhealthy, this field will contain an ISO8601 time stamp. Example: `2022-08-30T14:14:14.000Z` |
| `user`                   | The ID of the user that created the webhook                                                                                                                                  |
| `subscribed_event_types` | The event types that the webhook is subscribed to. See [possible event types here](#webhook-events).                                                                         |

## Get a Webhook

```sh
curl -X GET "https://api.cobalt.io/webhooks/YOUR-WEBHOOK-IDENTIFIER" \
  -H "Accept: application/vnd.cobalt.v2+json" \
  -H "Authorization: Bearer YOUR-PERSONAL-API-TOKEN" \
  -H "X-Org-Token: YOUR-V2-ORGANIZATION-TOKEN"
```

> Response Sample

```json
{
  "resource": {
    "id": "wb_38URp3gxZqfkjEXmkybrrs",
    "name": "My Webhook",
    "url": "https://example.local",
    "active": true,
    "unhealthy_since": null,
    "user": "us_RxvqT5T3WCFrfTF74B6JLC",
    "subscribed_event_types": [
      "PENTEST_CREATED",
      "PENTEST_STATE_UPDATED",
      "FINDING_DELETED",
      "FINDING_PUBLISHED",
      "FINDING_STATE_UPDATED",
      "FINDING_UPDATED"
    ]
  }
}
```

Returns a webhook that belongs to an organization.

{{% add-org-token %}}

### HTTP Request

`GET https://api.cobalt.io/webhooks/YOUR-WEBHOOK-IDENTIFIER`

### Response Parameters

| Name                  | Description                                                                                                                                                                       |
|------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `id`                     | The ID of the webhook                                                                                                                                                             |
| `name`                   | The name of the webhook                                                                                                                                                           |
| `url`                    | The URL that webhook events are sent to                                                                                                                                           |
| `active`                 | A boolean flag that indicates if the webhook is active                                                                                                                            |
| `unhealthy_since`        | The time that we began failing to deliver events to this webhook. If the webhook is unhealthy, this field will contain an ISO8601 time stamp. Example: `2022-08-30T14:14:14.000Z` |
| `user`                   | The ID of the user that created the webhook                                                                                                                                       |
| `subscribed_event_types` | [Event types](#webhook-events) that the webhook is subscribed to.                                                                         |

## Create a Webhook

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
            "secret": "my_secret",
            "url": "https://example.local/webhook",
            "subscribed_event_types": [
              "FINDING_PUBLISHED"
            ]
          }'
```

> {{% 201-code %}} The `Location` response header contains the URL of the new webhook within the Cobalt API.

Creates a new webhook for an organization.

When you attempt to create a webhook, we send a test event to your endpoint to validate the webhook.
Your endpoint must respond with a successful HTTP response status code, such as `200`, `201`, or `204`.
For details on test events, see [Webhook Events](./#webhook-events).

{{% add-org-token %}}

### HTTP Request

`POST https://api.cobalt.io/webhooks`

### Request Body

| Name                  | Description                                                                                                                                                                                                   |
|------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`                   | The name of the webhook. Use a unique name for each webhook within an organization.                          |
| `active`                 | A boolean flag specifying if the webhook is active                                                                                                                                                            |
| `secret`                 | An arbitrary string value. We include this value in the `X-Secret` header when we send webhook events to you. You can use this to verify that the events you receive are from Cobalt. This field is optional. |
| `url`                    | The URL to send events to                                                                                                                                                                                     |
| `subscribed_event_types` | The event types that the webhook should be subscribed to. May not be an empty list. See [possible event types here](#webhook-events).                                                                         |

### Response

{{% 201-code %}} The `Location` response header contains the URL of the new
webhook within the Cobalt API.

## Update a Webhook

```sh
curl -X PATCH 'https://api.cobalt.io/webhooks/YOUR-WEBHOOK-IDENTIFIER' \
  -H 'Accept: application/vnd.cobalt.v2+json' \
  -H 'Authorization: Bearer YOUR-PERSONAL-API-TOKEN' \
  -H 'Content-Type: application/vnd.cobalt.v2+json' \
  -H 'X-Org-Token: YOUR-V2-ORGANIZATION-TOKEN' \
  --data '{
            "name": "FooBar",
            "secret": "super_secret",
            "active": false,
            "url": "https://example.local/webhook2",
            "subscribed_event_types": [
              "FINDING_PUBLISHED"
            ]
          }'
```

> {{% 204-code %}}

Updates a webhook with the provided details.

{{% add-org-token %}}

### HTTP Request

`PATCH https://api.cobalt.io/webhooks/YOUR-WEBHOOK-IDENTIFIER`

### Request Body

All parameters in the request body are optional. Include the fields that you want to update.

| Name                  | Description                                                                                                                                                                                                                                                                                                    |
|------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`                   | The name of the webhook. Use a unique name for each webhook within an organization.                          |
| `secret`                 | An arbitrary string value. We include this value in the `X-Secret` header when we send webhook events to you. You can use this to verify that the events you receive are from Cobalt. To remove the secret, set the secret field to an empty string.                                                                                                                         |
| `active`                 | A boolean parameter specifying if the webhook is active.                                                                                                                                                                                                                                                             |
| `url`                    | The URL to send webhook events to.                                                                                                                                                                                                                                                                                      |
| `subscribed_event_types` | The event types that the webhook should be subscribed to. May not be an empty list. Non-specified event types that are currently subscribed to will be un-subscribed from. Specified event types that are not currently subscribed to will be subscribed to. See [possible event types here](#webhook-events). |

### Response

{{% 204-code %}}

## Delete a Webhook

```sh
curl -X DELETE 'https://api.cobalt.io/webhooks/YOUR-WEBHOOK-IDENTIFIER' \
  -H 'Accept: application/vnd.cobalt.v2+json' \
  -H 'Authorization: Bearer YOUR-PERSONAL-API-TOKEN' \
  -H 'Content-Type: application/vnd.cobalt.v2+json' \
  -H 'X-Org-Token: YOUR-V2-ORGANIZATION-TOKEN'
```

> {{% 204-code %}}

Deletes a webhook that belongs to an organization.

{{% add-org-token %}}

### HTTP Request

`DELETE https://api.cobalt.io/webhooks/YOUR-WEBHOOK-IDENTIFIER`

### Response

{{% 204-code %}} The response contains no data.

## Webhook Events

> Object Sample

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

Webhook event properties:

| Name         | Description                                |
|---------------|--------------------------------------------|
| `id`            | The ID of the webhook event                |
| `action`        | The action that the event is related to    |
| `subject`       | The subject that the event is related to   |
| `timestamp`     | The time that the event ocurred            |

`action` types:

* `FINDING_DELETED`
* `FINDING_PUBLISHED`
* `FINDING_STATE_UPDATED`
* `FINDING_UPDATED`
* `PENTEST_CREATED`
* `PENTEST_STATE_UPDATED`
* `TEST_EVENT`

`subject` properties:

| Name         | Description                                |
|---------------|--------------------------------------------|
| `id`            | The ID of the subject resource             |
| `type`          | The type of the subject resource           |

`subject` types:

* `TEST_EVENT`
* `PENTEST`
* `FINDING`

## Webhook Delivery and Health

Delivery process:

1. An event that you're subscribed to occurs on the Cobalt platform.
1. We attempt to send the event to your webhook endpoint through an HTTP POST request.
    * If your endpoint responds with a successful HTTP response status code, such as `200`, `201`, or `204`,
    we mark the delivery as successful.
    * If your endpoint doesn't respond with a successful HTTP response status code, we take the following steps.
1. We attempt to send the event 5 more times with an interval of 5 seconds between each request.
    * If the delivery is successful, we mark your webhook as healthy.
    * If none of the delivery attempts succeed, we mark your webhook endpoint
    as unhealthy and put the event into our failed events queue.
1. We attempt to redeliver failed events with an interval of one hour.
    * If your webhook endpoint becomes able to receive events again, we mark the webhook as healthy.
    * If your webhook endpoint stays unhealthy for 48 hours, we deactivate your webhook.

If your webhook becomes deactivated, reactivate it through the API.

## Best Practices

* Set your webhook secret to a high-entrophy value of sufficient length.
When you receive an event, verify that the value in the `X-Secret` header
matches your secret. This ensures that you do not process fraudulent
webhook events from a threat actor.
* Don't add expensive operations to the endpoint that receives webhook events.
A common pattern is to receive webhook events with a lightweight endpoint that
publishes received events to a message queue that can be processed by your components
containing business logic. This keeps the latency and failure rate of your webhook
endpoint low.
