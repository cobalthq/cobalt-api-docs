---
weight: 11
title: Webhooks
---

# Webhooks

Webhooks allow your system to be notified when events occur on the Cobalt Platform via HTTP POST requests.
This eliminates the need to poll the API for updates.
You can also manage your webhooks within the Integrations Hub in the Cobalt Platform.

## Get all webhooks

```sh
curl -X GET "https://api.us.cobalt.io/webhooks" \
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

This endpoint retrieves a list of all webhooks that belong to your organization.

### HTTP Request

`GET https://api.us.cobalt.io/webhooks`

### URL Parameters

| Parameter | Default | Description                                                                                                  |
|-----------|---------|--------------------------------------------------------------------------------------------------------------|
| `cursor`  | N/A     | Used for [pagination](./#pagination). Example: `https://api.us.cobalt.io/webhooks?cursor=a1b2c3d4`              |
| `limit`   | `10`    | If specified, returns only a specified amount of webhooks. Example: `https://api.us.cobalt.io/webhooks?limit=5` |

### Response Fields

| Field                  | Description                                                                                                                                                                  |
|------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                     | The ID of the webhook                                                                                                                                                        |
| name                   | The name of the webhook                                                                                                                                                      |
| url                    | The URL that webhook events are sent to                                                                                                                                      |
| active                 | A boolean flag that indicates if the webhook is active                                                                                                                       |
| unhealthy_since        | The time that we began failing to deliver events to this webhook. If the webhook is unhealthy, this field will contain an ISO8601 time stamp. Ex: `2022-08-30T14:14:14.000Z` |
| user                   | The ID of the user that created the webhook                                                                                                                                  |
| subscribed_event_types | The event types that the webhook is subscribed to. See [possible event types here](#webhook-events).                                                                         |

## Get a webhook

```sh
curl -X GET "https://api.us.cobalt.io/webhooks/YOUR-WEBHOOK-IDENTIFIER" \
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

This endpoint retrieves a specific webhook belonging to your organization.

### HTTP Request

`GET https://api.us.cobalt.io/webhooks/YOUR-WEBHOOK-IDENTIFIER`

### Response Fields

| Field                  | Description                                                                                                                                                                       |
|------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                     | The ID of the webhook                                                                                                                                                             |
| name                   | The name of the webhook                                                                                                                                                           |
| url                    | The URL that webhook events are sent to                                                                                                                                           |
| active                 | A boolean flag that indicates if the webhook is active                                                                                                                            |
| unhealthy_since        | The time that we began failing to deliver events to this webhook. If the webhook is unhealthy, this field will contain an ISO8601 time stamp. Example: `2022-08-30T14:14:14.000Z` |
| user                   | The ID of the user that created the webhook                                                                                                                                       |
| subscribed_event_types | The event types that the webhook is subscribed to. See [possible event types here](#webhook-events)                                                                               |

<aside class="notice">
Remember - you can only request a webhook scoped to the organization specified in the <code>X-Org-Token</code> header.
</aside>

## Create a webhook

```sh
curl -X POST "https://api.us.cobalt.io/webhooks" \
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

> The above command returns the details of the created webhook and a `201` response code when successful.
> There will be a `Location` header pointing at the newly created webhook.

```json
{
  "resource": {
    "id": "wb_38URp3gxZqfkjEXmkybrrs",
    "name": "My Webhook",
    "url": "https://example.local/webhook",
    "active": true,
    "unhealthy_since": null,
    "user": "us_RxvqT5T3WCFrfTF74B6JLC",
    "subscribed_event_types": [
      "FINDING_PUBLISHED"
    ]
  }
}
```

This endpoint creates a new webhook belonging to your organization.

When you attempt to create a webhook, we will send a test event to your endpoint to validate that events
can be delivered successfully. Your endpoint must respond with a successful HTTP response status code,
for example, 200, 201, 204, etc. For details on test events, see the [Webhook Events](./#webhook-events) section below.

### HTTP Request

`POST https://api.us.cobalt.io/webhooks`

### Body

| Field                  | Description                                                                                                                                                                                                   |
|------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| name                   | The name of the webhook                                                                                                                                                                                       |
| active                 | A boolean flag specifying if the webhook is active                                                                                                                                                            |
| secret                 | An arbitrary string value. We include this value in the `X-Secret` header when we send webhook events to you. You can use this to verify that the events you receive are from Cobalt. This field is optional. |
| url                    | The URL to send events to                                                                                                                                                                                     |
| subscribed_event_types | The event types that the webhook should be subscribed to. May not be an empty list. See [possible event types here](#webhook-events).                                                                         |

### Response

When the request is successful, you get a `201` response code and the details of the created webhook.
The response body fields are the same as documented [here](#get-a-webhook).
The `Location` response header contains the URL of the new webhook within the Cobalt API.

<aside class="notice">
Multiple webhooks may not have the same name or URL within an organization.
</aside>

<aside class="notice">
Remember - you can only create a webhook within the organization specified in the <code>X-Org-Token</code> header.
</aside>

## Update a webhook

```sh
curl -X PATCH 'https://api.us.cobalt.io/webhooks/YOUR-WEBHOOK-IDENTIFIER' \
  -H 'Accept: application/vnd.cobalt.v2+json' \
  -H 'Authorization: Bearer YOUR-PERSONAL-API-TOKEN' \
  -H 'Content-Type: application/vnd.cobalt.v2+json' \
  -H 'Idempotency-Key: A-UNIQUE-IDENTIFIER-TO-PREVENT-UNINTENTIONAL-DUPLICATION' \
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

> The above command returns the details of the updated webhook and a `200` response code when successful.

```json
{
  "resource": {
    "id": "wb_38URp3gxZqfkjEXmkybrrs",
    "name": "FooBar",
    "url": "https://example.local/webhook2",
    "active": false,
    "unhealthy_since": null,
    "user": "us_RxvqT5T3WCFrfTF74B6JLC",
    "subscribed_event_types": [
      "FINDING_PUBLISHED"
    ]
  }
}
```

This endpoint updates a webhook belonging to your organization.

### HTTP Request

`PATCH https://api.us.cobalt.io/webhooks/YOUR-WEBHOOK-IDENTIFIER`

### Body

All body fields are optional. You only need to include the fields that should be updated.

| Field                  | Description                                                                                                                                                                                                                                                                                                    |
|------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| name                   | The name of the webhook                                                                                                                                                                                                                                                                                        |
| secret                 | An arbitrary string value. We include this value in the `X-Secret` header when we send webhook events to you. You can use this to verify that the events you receive are from Cobalt.                                                                                                                          |
| active                 | A boolean flag specifying if the webhook is active                                                                                                                                                                                                                                                             |
| url                    | The URL to send events to                                                                                                                                                                                                                                                                                      |
| subscribed_event_types | The event types that the webhook should be subscribed to. May not be an empty list. Non-specified event types that are currently subscribed to will be un-subscribed from. Specified event types that are not currently subscribed to will be subscribed to. See [possible event types here](#webhook-events). |

### Response

On a successful update, a `200` response code and the details of the updated webhook will be returned.
The response body fields are the same as documented [here](#get-a-webhook).

<aside class="notice">
To remove the secret, set the secret field to an empty string.
</aside>

<aside class="notice">
Multiple webhooks may not have the same name or URL within an organization.
</aside>

<aside class="notice">
Remember - you can only update a webhook within the organization specified in the <code>X-Org-Token</code> header.
</aside>

## Delete a webhook

```sh
curl -X DELETE 'https://api.us.cobalt.io/webhooks/YOUR-WEBHOOK-IDENTIFIER' \
  -H 'Accept: application/vnd.cobalt.v2+json' \
  -H 'Authorization: Bearer YOUR-PERSONAL-API-TOKEN' \
  -H 'Content-Type: application/vnd.cobalt.v2+json' \
  -H 'X-Org-Token: YOUR-V2-ORGANIZATION-TOKEN'
```

> The above command returns no data and a `204` response code when successful.

This endpoint deletes a webhook belonging to your organization.

### HTTP Request

`DELETE https://api.us.cobalt.io/webhooks/YOUR-WEBHOOK-IDENTIFIER`

### Response

On successful deletion, a `204` response code will be returned.

<aside class="notice">
Remember - you can only delete a webhook within the organization specified in the <code>X-Org-Token</code> header.
</aside>

## Webhook Events

Webhook event properties:

| Field         | Nullable | Description                                          |
|---------------|----------|------------------------------------------------------|
| id            | false    | The ID of the webhook event                          |
| action        | false    | The action that the event is related to              |
| subject       | false    | The subject that the event is related to             |
| details       | true     | An object containing additional details of the event |
| timestamp     | false    | The time that the event occurred                     |

`action` types:

* `FINDING_DELETED`
* `FINDING_PUBLISHED`
* `FINDING_STATE_UPDATED`
* `FINDING_UPDATED`
* `PENTEST_CREATED`
* `PENTEST_STATE_UPDATED`
* `TEST_EVENT`

`subject` properties:

| Field         | Nullable | Description                                         |
|---------------|----------|-----------------------------------------------------|
| id            | false    | The ID of the subject resource                      |
| type          | false    | The type of the subject resource                    |
| associations  | true     | An object containing the IDs of associated entities |

`subject` types:

* `TEST_EVENT`
* `PENTEST`
* `FINDING`

The format of the subject ID will change based on the type of the subject.
The full information about the event subject can be fetched from the `GET` API route that
is appropriate for the subject type.

Examples:

* A `FINDING_PUBLISHED` event would have a subject ID with the format: `vl_xxxxxxxxxxxxxxxxxxxxxx`.
  The full information about the finding that was published can be found by making a `GET`
  request to the API endpoint: `/findings/vl_xxxxxxxxxxxxxxxxxxxxxx`.
* A `PENTEST_CREATED` event would have a subject ID with the format: `pt_xxxxxxxxxxxxxxxxxxxxxx`.
  The full information about the pentest that was created can be found by making a `GET`
  request to the API endpoint: `/pentests/pt_xxxxxxxxxxxxxxxxxxxxxx`.

```json
{
  "id": "eve_Rg7m1DgCeXcRbsyzB4KPYA",
  "action": "PENTEST_CREATED",
  "subject": {
    "id": "pt_BepESWncwNyzgs7x1go4Ts",
    "type": "PENTEST",
    "associations": {
      "asset_id": "as_GZgcehapJUNh6mjNuqsE4T"
    }
  },
  "details": null,
  "timestamp": "2023-07-25T19:30:40.009Z"
}
```

## Webhook Delivery and Health

Delivery process:

* An event occurs on the Cobalt Platform that you are subscribed to
* Cobalt will attempt to send the event to your webhook endpoint via an HTTP POST
request. If your endpoint responds with a successful HTTP response status code, for example, 200, 201, or 204,
then we will mark the delivery as successful.
* If your endpoint does not respond with a successful HTTP status, then we will attempt
to send the event 5 more times with 5 seconds between each request.
* If none of the delivery attempts succeed, then we will mark your webhook endpoint
as unhealthy and put the event into our failed events queue.
* On an hourly interval we will attempt to redeliver failed events.
* If your webhook endpoint becomes able to receive events again, we will mark your
webhook endpoint as healthy.
* If your webhook endpoint stays unhealthy for 48 hours then we will deactivate your webhook.

If your webhook becomes deactivated then you will need to activate it again via the user interface or the API.

## Best Practices

1. Set your webhook secret to a high-entrophy value of sufficient length.
When you receive an event, check that the value in the `X-Secret` header
matches your secret. This ensures that you do not process fraudulent
webhook events from a threat actor.
2. Don't add expensive operations to the endpoint that receives webhook events.
A common pattern is to receive webhook events with a lightweight endpoint that
publishes received events to a message queue that can be processed by your components
containing business logic. This keeps the latency and failure rate of your webhook
endpoint low.
