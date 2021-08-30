---
weight: 14
title: Findings
---

# Findings

## Get All Findings

```shell
curl -X GET "https://api.cobalt.io/findings" \
  -H "accept: application/vnd.cobalt.v1+json" \
  -H "Authorization: Bearer your-personal-api-token-here" \
  -H "X-Org-Token: your-org-token-here"
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
        "labels": [
          {
            "name": "Your label"
          }
        ],
        "impact": 5,
        "likelihood": 4,
        "severity": "high",
        "affected_targets": [ ""],
        "proof_of_concept": null,
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
          },
          {
            "action": "impact_changed",
            "value": 5,
            "timestamp": "2021-04-01T15:14:05.856Z"
          },
          {
            "action": "state_changed",
            "value": "need_fix",
            "timestamp": "2021-04-01T15:14:06.757Z"
          },
          {
            "action": "state_changed",
            "value": "check_fix",
            "timestamp": "2021-04-01T15:14:57.845Z"
          }
        ],
        "state": "check_fix"
      },
      "links": {
        "ui": {
          "url": "https://api.cobalt.io/links/long-web-app-redirect-to-this-finding"
        }
      }
    }
 ]
}

```

This endpoint retrieves a list of all pentest findings that belong to the org specified in the header, filterable by `pentest_id` or `asset_id`. The `log` array presents a history of each finding and corresponding timestamp. 

### Calculations

*Cobalt Risk Input Fields*
 - Risk = Impact * Likelihood
 - `impact` := [1-5]
 - `likelihood` := [1-5]

*Cobalt Risk Classification*
 - `severity` (aka `criticality`) :=
 - **high** = Risk @ 16+
 - **medium** = Risk @ 5-15
 - **low** = Risk @ 1-4


### HTTP Request

`GET https://api.cobalt.io/findings`

### Fields

Field           | Enum Types
--------------- | -----------
`log`           | created, impact_changed, likelihood_changed, state_changed
`severity`      | null, low, medium, high  (`severity`, aka `criticality` in our web app, will be null for findings where their likelihood/impact have not yet been set)
`state`         | new, triaging, need_fix, wont_fix, valid_fix, check_fix, invalid, carried_over
`type_category` | XSS, SQLi, ... (about 30 more via the Cobalt Taxonomy)
`url`           | The links.ui.url will redirect an authorized user to this finding in the Cobalt platform


<aside class="success">
Remember — you can only request Findings scoped to the Org specified in the header.
</aside>
