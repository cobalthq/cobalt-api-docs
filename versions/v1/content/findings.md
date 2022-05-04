---
weight: 6
title: Findings
---

# Findings

## Get All Findings

```sh
curl -X GET "https://api.cobalt.io/findings" \
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
  ],
  "pagination": {
    "next_page": "/findings?cursor=a1b2c3d4",
    "prev_page": "/findings?cursor=4d3c2b1a"
  }
}
```

This endpoint retrieves a list of all pentest findings that belong to the org specified in the header, filterable by
`pentest_id` or `asset_id`. The `log` array presents a history of each finding and corresponding timestamp.

### Calculations

We follow the standard risk model described by OWASP, where:

`Risk = Impact * Likelihood`

Cobalt Risk Input Fields:

- `impact` := [1-5]
- `likelihood` := [1-5]

Cobalt Risk Classification (`severity`, a.k.a. `criticality`):

| Category        | Score | Description                                                                                                                                                     |
|-----------------|-------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `critical`      | 25    | Includes vulnerabilities that require immediate attention.                                                                                                      |
| `high`          | 16-24 | Impacts the security of your application/platform/hardware, including supported systems. Includes high probability vulnerabilities with a high business impact. |
| `medium`        | 5-15  | Includes vulnerabilities that are: medium risk, medium impact; low risk, high impact; high risk, low impact.                                                    |
| `low`           | 2-4   | Specifies common vulnerabilities with minimal impact.                                                                                                           |
| `informational` | 1     | Notes vulnerabilities of minimal risk to your business.                                                                                                         |

### HTTP Request

`GET https://api.cobalt.io/findings`

### URL Parameters

| Parameter | Default | Description                                                                                              |
|-----------|---------|----------------------------------------------------------------------------------------------------------|
| `cursor`  | N/A     | Used for [pagination](./#pagination), e.g. `https://api.cobalt.io/findings?cursor=a1b2c3d4`              |
| `limit`   | `1000`  | If specified, returns only a specified amount of findings, e.g. `https://api.cobalt.io/findings?limit=5` |

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
Remember — you can only request Findings scoped to the Org specified in the header.
</aside>
