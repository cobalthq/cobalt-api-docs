---
weight: 7
title: Get Specific Findings
---

## Get Specific Findings

```sh
curl -X GET "https://api.cobalt.io/findings?pentest=pt_9Ig1234" \
  -H "Accept: application/vnd.cobalt.v1+json" \
  -H "Authorization: Bearer YOUR-PERSONAL-API-TOKEN" \
  -H "X-Org-Token: YOUR-V1-ORGANIZATION-TOKEN"
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "resource": {
        "id": "vu_ZzZuekb",
        "tag": "#PT3334_37",
        "title": "XSS vulnerability",
        "description": "Cross-Site Scripting (XSS) attacks are a type of injection, in which malicious scripts...",
        "type_category": "Cross-Site Scripting (XSS)",
        "labels": [
          {
            "name": "Your label"
          }
        ],
        "impact": 4,
        "likelihood": 4,
        "severity": "high",
        "affected_targets": [
          "https://example.com",
          "192.168.1.1"
        ],
        "proof_of_concept": "Here you can see...",
        "suggested_fix": "Ensure this...",
        "pentest_id": "pt_9Ig1234",
        "asset_id": "as_cwrsqsL",
        "log": [
          {
            "action": "created",
            "timestamp": "2021-04-01T15:13:24.322Z"
          },
          {
            "action": "likelihood_changed",
            "value": 4,
            "timestamp": "2021-04-01T15:14:05.856Z"
          }
        ],
        "state": "need_fix"
      },
      "links": {
        "ui": {
          "url": "https://api.cobalt.io/links/eyJ0eXBlIjoic29tZXRoaW5nIiwib3JnU2x1ZyI6ImNvYmFsdCIsInBlbnRlc3RUYWciOiJz="
        }
      }
    }
  ]
}
```

You can filter for findings scoped to a specific pentest or asset.

### HTTP Requests

`GET https://api.cobalt.io/findings?pentest=pt_9Ig1234`

`GET https://api.cobalt.io/findings?asset=as_cwrsqsL`

### URL Parameters

| Parameter | Default | Description                                                                                                        |
|-----------|---------|--------------------------------------------------------------------------------------------------------------------|
| `pentest` | N/A     | If specified, returns findings scoped to this pentest id, e.g. `https://api.cobalt.io/findings?pentest=pt_9Ig1234` |
| `asset`   | N/A     | If specified, returns findings scoped to this asset id, e.g. `https://api.cobalt.io/findings?asset=as_cwrsqsL`     |
