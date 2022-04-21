---
weight: 8
title: Get Specific Findings
---

# Findings

## Get One Finding

```sh
curl -X GET "https://api.cobalt.io/findings/your-finding-identifier" \
  -H "accept: application/vnd.cobalt.v2+json" \
  -H "Authorization: Bearer your-personal-api-token-here" \
  -H "X-Org-Token: your-org-token-here"
```

> The above command returns JSON structured like this:

```json
{
  "resource": {
    "id": "your-finding-identifier",
    "tag": "#PT5940",
    "title": "Finding Title",
    "description": "A finding description",
    "type_category": "type",
    "labels": [],
    "impact": null,
    "likelihood": null,
    "severity": null,
    "affected_targets": [
      "dsfa"
    ],
    "proof_of_concept": "a proof of concept",
    "suggested_fix": "a suggestion fix",
    "pentest_id": "an_pentest_identifier",
    "asset_id": "an_asset_identifier",
    "log": [
      {
        "action": "created",
        "timestamp": "2021-09-22T18:43:01.677Z"
      }
    ],
    "state": "new"
  },
  "links": {
    "ui": {
      "url": "https://api.cobalt.io/links/long-web-app-redirect-to-this-pentest"
    }
  }
}
```

This endpoint retrieves a specific Finding that belong to the Org specified in the header.

### HTTP Request

`GET https://api.cobalt.io/findings/your-finding-identifier-here`

### Response Fields

| Field           | Enum Types                                                                                                             |
|-----------------|------------------------------------------------------------------------------------------------------------------------|
| `log`           | created, impact_changed, likelihood_changed, state_changed                                                             |
| `severity`      | null, low, medium, high  (aka `criticality`. will be null if likelihood/impact have not yet been set by the pentester) |
| `state`         | new, triaging, need_fix, wont_fix, valid_fix, check_fix, invalid, carried_over                                         |
| `type_category` | XSS, SQLi, ... (about 30 more via the Cobalt Taxonomy)                                                                 |
| `url`           | The links.ui.url will redirect an authorized user to this finding in the Cobalt platform                               |

### State

- `new`: The finding has been created but not yet triaged.
- `triaging`: The finding is being evaluated.
- `need_fix`: The finding was deemed valid and a fix either is being developed or will be developed in the future.
- `wont_fix`: The finding was deemed valid but immaterial or meaningless and will not be addressed.
- `check_fix`: A fix has been applied and now is awaiting validation by the pentester.
- `invalid`: The finding was rejected as not being a true vulnerability.
- `carried_over`: The finding was carried over from a previous pentest.


<aside class="success">
Remember — you can only request a Finding scoped to the Org specified in the header.
</aside>
