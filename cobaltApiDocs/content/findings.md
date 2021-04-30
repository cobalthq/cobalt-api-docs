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
        "type_category": null,
        "labels": [],
        "impact": 4,
        "likelihood": 4,
        "severity": "high",
        "affected_targets": [ ""],
        "proof_of_concept": null,
        "suggested_fix": "Ensure this...",
        "pentest_id": "pt_9Ig1234",
        "asset_id": "as_cwrsqsL",
        "log": [],
        "state": "need_fix"
      }
    }
 ]
}

```

This endpoint retrieves a list of all pentest findings that belong to the org specified in the header, filterable by pentest id or asset id.

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
`severity`      | null, low, medium, high  (`severity`, aka `criticality` in our web app, will be null for findings where their likelihood/impact have not yet been set)
`state`         | new, triaging, need_fix, wont_fix, valid_fix, check_fix, invalid, carried_over
`type_category` | XSS, SQLi, ... (about 30 more via the Cobalt Taxonomy)


<aside class="success">
Remember — you can only request Findings scoped to the Org specified in the header.
</aside>
