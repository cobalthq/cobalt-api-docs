---
weight: 7
title: Get Specific Findings
---

## Get Specific Findings

```sh
curl -X GET "https://api.cobalt.io/findings?pentest=pt_9Ig" \
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
        "id": "vu_2wXY3bq",
        "tag": "#PT3334_37",
        "title": "SQL Injection",
        "description": "A SQL injection attack...",
        "type_category": "SQL Injection",
        "labels": [],
        "impact": 4,
        "likelihood": 4,
        "severity": "high",
        "affected_targets": [ ""],
        "proof_of_concept": null,
        "suggested_fix": "Ensure this...",
        "pentest_id": "pt_9Ig",
        "asset_id": "as_cwrsqsL",
        "log": [],
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

`GET https://api.cobalt.io/findings?pentest=pt_9Ig`

`GET https://api.cobalt.io/findings?asset=as_cwrsqsL`

### URL Parameters

| Parameter | Default | Description                                                                                                    |
|-----------|---------|----------------------------------------------------------------------------------------------------------------|
| `pentest` | N/A     | If specified, returns findings scoped to this pentest id, e.g. `https://api.cobalt.io/findings?pentest=pt_9Ig` |
| `asset`   | N/A     | If specified, returns findings scoped to this asset id, e.g. `https://api.cobalt.io/findings?asset=as_cwrsqsL` |
