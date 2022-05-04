---
weight: 8
title: Events
---

# Events

## Get All Events

```sh
curl -X GET "https://api.cobalt.io/events" \
  -H "Accept: application/vnd.cobalt.v1+json" \
  -H "Authorization: Bearer YOUR-PERSONAL-API-TOKEN"
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
  ],
  "pagination": {
    "next_page": "/events?cursor=123asdzxc",
    "prev_page": "/events?cursor=123asdzxd"
  }
}
```

This endpoint retrieves a list of all events for your account.

### HTTP Request

`GET https://api.cobalt.io/events`

### URL Parameters

| Parameter | Default | Description                                                                                |
|-----------|---------|--------------------------------------------------------------------------------------------|
| cursor    | N/A     | Used for [pagination](./#pagination), e.g. `https://api.cobalt.io/events?cursor=123asdzxc` |
| limit     | `10`    | If specified, returns only `limit` events, e.g. `https://api.cobalt.io/events?limit=5`     |
