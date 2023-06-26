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

> Response Sample

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
        },
        "timestamp": "2022-05-03T01:34:21.587Z"
      }
    },
    {
      "resource": {
        "id": "277600",
        "action": "pentest_deleted",
        "subject": {
          "id": "277600",
          "type": "program"
        },
        "timestamp": "2022-05-03T01:34:21.587Z"
      }
    },
    {
      "resource": {
        "id": "277567",
        "action": "finding_created",
        "subject": {
          "id": "277567",
          "type": "vulnerability"
        },
        "timestamp": "2022-05-03T01:34:21.587Z"
      }
    }
  ],
  "pagination": {
    "next_page": "/events?cursor=a1b2c3d4",
    "prev_page": "/events?cursor=4d3c2b1a"
  }
}
```

Returns all events for your account.

### HTTP Request

`GET https://api.cobalt.io/events`

### Query Parameters

| Name | Default | Description                                                                                                 |
|-----------|---------|-------------------------------------------------------------------------------------------------------------|
| `cursor`  | N/A     | {{% cursor %}} Example: `https://api.cobalt.io/events?cursor=a1b2c3d4`            |
| `limit`   | `10`    | {{% limit %}} Example: `https://api.cobalt.io/events?limit=5` |
