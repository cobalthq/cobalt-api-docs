---
weight: 10
title: Events
---

# Events

## Get All Events

```sh
curl -X GET "https://api.us.cobalt.io/events" \
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
          "id": "ac_Y35JcpGoakrjUSVjtVpXyH",
          "type": "comment"
        },
        "timestamp": "2022-05-03T01:34:21.587Z"
      }
    },
    {
      "resource": {
        "id": "ac_Y35JcpGoakrjUSVjtVpXyP",
        "action": "pentest_deleted",
        "subject": {
          "id": "ac_Y35JcpGoakrjUSVjtVpXyP",
          "type": "program"
        },
        "timestamp": "2022-05-03T01:34:21.587Z"
      }
    },
    {
      "resource": {
        "id": "ac_Y35JcpGoakrjUSVjtVpXyX",
        "action": "finding_created",
        "subject": {
          "id": "ac_Y35JcpGoakrjUSVjtVpXyX",
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

This endpoint retrieves a list of all events for your account.

### HTTP Request

`GET https://api.us.cobalt.io/events`

### URL Parameters

| Parameter | Default | Description                                                                                              |
|-----------|---------|----------------------------------------------------------------------------------------------------------|
| `cursor`  | N/A     | Used for [pagination](./#pagination). Example: `https://api.us.cobalt.io/events?cursor=a1b2c3d4`            |
| `limit`   | `10`    | If specified, returns only a specified amount of events. Example: `https://api.us.cobalt.io/events?limit=5` |
