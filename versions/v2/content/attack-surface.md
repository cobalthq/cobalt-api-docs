---
weight: 14
title: "Attack Surface"
---

# Attack Surface

## Get Attack Surface Stats

```sh
curl --location 'https://api.us.cobalt.io/attack_surface/stats' \
  -H "Accept: application/vnd.cobalt.v2+json" \
  -H "Authorization: Bearer YOUR-PERSONAL-API-TOKEN" \
  -H "X-Org-Token: YOUR-V2-ORGANIZATION-TOKEN"
  --data '{}'
```

> The above command returns JSON structured like this:

```json
{
      "resource": {
        "domains": "3",
        "seen_hosts": "200",
        "new_seen_hosts": "10"
      }
}
```

This endpoint retrieves stats from Attack Surface for the organization

### HTTP Request

`GET https://api.us.cobalt.io/attack_surface/stats`

### Response Fields

| Field           | Description                                                                         |
|-----------------|-------------------------------------------------------------------------------------|
| `domains`      | Total amount of domains                             |
| `seen_hosts`    | Amount of hosts with at least one IP found within the last 7 days                                                  |
| `new_seen_hosts`     | Amount of hosts we found an IP for the first time within the last 7 days              |

