---
weight: 10
title: Engagements
---

# Engagements

## Get All Engagements

```sh
curl -X GET "https://api.us.cobalt.io/engagements" \
  -H "Accept: application/vnd.cobalt.v2+json" \
  -H "Authorization: Bearer YOUR-PERSONAL-API-TOKEN" \
  -H "X-Org-Token: YOUR-V2-ORGANIZATION-TOKEN"
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "resource": {
        "engagement_type": "secure_code_review",
        "id": "scr_BXc7VWbtrUMHE4Wak95Le",
        "tag": "#SCR26728",
        "title": "Secure Code Review - Public API",
        "methodology": "code_review",
        "state": "live",
        "start_date": "May 17 2024",
        "end_date": "May 24 2024",
        "asset_public_ids": [
          "as_A7EhhrnMZxSvfQPLqSFbE7"
        ]
      },
      "links": {
        "ui": {
          "url": "https://api.us.cobalt.io/links/eyJ0eXBlIjoiRU5HQUdFTUVOVCIsIm9yZ1NsdWciOiJtb2hyLXdhbGtlci05IiwicGVudGVzdFRhZyI6IiIsImZpbmRpbmdJZCI6IiIsImFzc2V0VGFnIjoiIiwiZW5nYWdlbWVudElkIjoiZHJhXzRCZWdtY3BIajRTUlJ1amlpUkxhdWsiLCJkYXN0VGFyZ2V0SWQiOiIiLCJkYXN0RmluZGluZ0lkIjoiIiwiZW5nYWdlbWVudEZpbmRpbmdJZCI6IiJ9"
        }
      }
    }
  ],
  "pagination": {
    "next_page": "/engagements?cursor=eyJwYWdlIjozLCJzaXplIjoxMH0=",
    "prev_page": "/engagements?cursor=eyJwYWdlIjoxLCJzaXplIjoxMH0="
  }
}
```

This endpoint retrieves a list of all engagements that belong to the organization specified in the `X-Org-Token` header.

### HTTP Request

`GET https://api.us.cobalt.io/engagements`

### URL Parameters

| Parameter | Default      | Description                                                                                                                                                                                                                                                                                  |
|-----------|--------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `cursor`  | N/A          | Used for [pagination](./#pagination). Example: `https://api.us.cobalt.io/engagements?cursor=eyJwYWdlIjoyLCJzaXplIjoxMH0=`                                                                                                                                                                    |
| `sort`    | `created_at` | If specified, returns engagements sorted in ascending order by one of these properties: `created_at`, `end_date`, `start_date`, `state`, or `updated_at`. To sort in descending order, use a `-` before the sort property. Example: `https://api.us.cobalt.io/engagements?sort=-start_date`. |

### Response Fields

| Field              | Description                                                                            |
|--------------------|----------------------------------------------------------------------------------------|
| `asset_public_ids` | List of the IDs of any assets associated with the returned engagement                  |
| `end_date`         | The ending date of the engagement. Format: Aug 25 2024                                 |
| `engagement_type`  | The engagement type. `digital_risk_assessment` or `secure_code_review`                 |
| `id`               | A unique ID representing the engagement                                                |
| `methodology`      | Engagement methodology. Valid values depend on the engagement type                     |
| `start_date`       | The starting date of the engagement. Format: Aug 11 2024                               |
| `state`            | `draft`, `in_review`, `planned`, `live`, `remediation`, `closed`, or `cancelled`       |
| `tag`              | A human-friendly unique ID representing the engagement                                 |
| `title`            | The title of the returned engagement                                                   |
| `links.ui.url`     | A link to redirect an authorized user to this engagement in the Cobalt web application |

<aside class="notice">
Remember - you can only request engagements scoped to the organization specified in the <code>X-Org-Token</code> header.
</aside>

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
| `tag`                 | All                      | A human-friendly unique ID representing the engagement                                 |
| `title`               | All                      | The title of the returned engagement                                                   |
| `links.ui.url`        | All                      | A link to redirect an authorized user to this engagement in the Cobalt web application |

<aside class="notice">
Remember - you can only request an engagement scoped to the organization specified in the <code>X-Org-Token</code> header.
</aside>
