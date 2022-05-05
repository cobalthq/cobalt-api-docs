---
weight: 10
title: Events
---

# Events

## Get All Events

```sh
curl -X GET "https://api.cobalt.io/events" \
  -H "Accept: application/vnd.cobalt.v2+json" \
  -H "Authorization: Bearer YOUR-PERSONAL-API-TOKEN"
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "resource": {
        "id": "ac_Y35JcpGoakrjUSVjtVpXyH",
        "action": "comment_created",
        "subject": {
          "id": "ac_xxxxxxxxxxx",
          "type": "comment"
        }
      }
    },
    {
      "resource": {
        "id": "ac_Y35JcpGoakrjUSVjtVpXyH",
        "action": "pentest_deleted",
        "subject": {
          "id": "ac_xxxxxxxxxxx",
          "type": "program"
        }
      }
    },
    {
      "resource": {
        "id": "ac_xxxxxxxxxxx",
        "action": "finding_created",
        "subject": {
          "id": "ac_xxxxxxxxxxx",
          "type": "vulnerability"
        }
      }
    }
  ],
  "pagination": {
    "next_page": "/events?cursor=a1b2c3d4",
    "prev_page": "/events?cursor=4d3c2b1a"
  }
}
```

This endpoint retrieves a list of all events for your account.

### HTTP Request

`GET https://api.cobalt.io/events`

### URL Parameters

| Parameter | Default | Description                                                                                          |
|-----------|---------|------------------------------------------------------------------------------------------------------|
| `cursor`  | N/A     | Used for [pagination](./#pagination), e.g. `https://api.cobalt.io/events?cursor=a1b2c3d4`            |
| `limit`   | `10`    | If specified, returns only a specified amount of events, e.g. `https://api.cobalt.io/events?limit=5` |
