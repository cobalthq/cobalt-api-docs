---
weight: 10
title: Engagements
---

# Engagements

## Get an Engagement

```sh
curl -X GET "https://api.us.cobalt.io/engagements/YOUR-ENGAGEMENT-IDENTIFIER" \
  -H "Accept: application/vnd.cobalt.v2+json" \
  -H "Authorization: Bearer YOUR-PERSONAL-API-TOKEN" \
  -H "X-Org-Token: YOUR-V2-ORGANIZATION-TOKEN"
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "resource": {
      "engagement_type": "secure_code_review",
      "id": "scr_Q2SX4qz3fTcJwAAiqRG5wp",
      "tag": "#SCR5940",
      "title": "HR System Secure Code Review 2022-Q4",
      "application_details": "",
      "objectives": "",
      "approach": "",
      "methodology": "code_review",
      "state": "live",
      "start_date": "Aug 11 2024",
      "end_date": "Aug 25 2024",
      "asset_public_ids": [
        "as_4L4ZjKgfzP7VBwUmqCZmmL"
      ],
    },
    "links": {
      "ui": {
        "url": "https://api.us.cobalt.io/links/eyJ0eXBlIjoiRU5HQUdFTUVOVCIsIm9yZ1NsdWciOiJtb2hyLXdhbGtlci05IiwicGVudGVzdFRhZyI6IiIsImZpbmRpbmdJZCI6IiIsImFzc2V0VGFnIjoiIiwiZW5nYWdlbWVudElkIjoic2NyX1EyU1g0cXozZlRjSndBQWlxUkc1d3AifQ=="
      }
    }
  }
}
```

This endpoint retrieves a specific engagement that belongs to the organization specified in the `X-Org-Token` header.

### HTTP Request

`GET https://api.us.cobalt.io/engagements/YOUR-ENGAGEMENT-IDENTIFIER-HERE`

### Response Fields

The fields that are returned depend on the engagement type.  This can be determined from the `engagement_type` field,
which is common to all engagement types.

| Field                 | Engagement Type(s)       | Description                                                                            |
|-----------------------|--------------------------|----------------------------------------------------------------------------------------|
| `activities`          | Digital risk assessments | Description of activities performed as part of the engagement                          |
| `application_details` | Secure code reviews      | Description of the application being reviewed                                          |
| `approach`            | Secure code reviews      | Description of the approach the reviewer should take                                   |
| `asset_public_id`     | All                      | List of the IDs of any assets targeted by the returned engagement                      |
| `end_date`            | All                      | The ending date of the engagement. Format: Aug 25 2024                                 |
| `engagement_type`     | All                      | The engagement type. `digital_risk_assessment` or `secure_code_review`                 |
| `id`                  | All                      | A unique ID representing the engagement                                                |
| `methodology`         | All                      | Engagement methodology. Valid values depend on the engagement type                     |
| `objectives`          | All                      | The objectives of the engagement. for example "Coverage of OWASP Top 10"               |
| `start_date`          | All                      | The starting date of the engagement. Format: Aug 11 2024                               |
| `state`               | All                      | `draft`, `in_review`, `planned`, `live`, `remediation`, `closed`, or `cancelled`       |
| `tag`                 | All                      | A human-friendly unique ID representating the engagement                               |
| `title`               | All                      | The title of the returned engagement                                                   |
| `links.ui.url`        | All                      | A link to redirect an authorized user to this engagement in the Cobalt web application |

<aside class="notice">
Remember - you can only request an engagement scoped to the organization specified in the <code>X-Org-Token</code> header.
</aside>
