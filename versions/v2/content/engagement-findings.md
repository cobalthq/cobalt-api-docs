---
weight: 11
title: Engagement Findings
---

# Engagement Findings

## States

The table below describes how the engagement finding state values used by the API correspond to finding states shown in
the user interface.

| API Value    | UI Name          | Description                                                                       |
|--------------|------------------|-----------------------------------------------------------------------------------|
| new          | Draft            | A pentester has created a draft finding but has not yet submitted it for triaging |
| triaging     | Triaging         | The finding is being triaged                                                      |
| need_fix     | Pending Fix      | The finding is valid and needs to be fixed                                        |
| check_fix    | Ready for Retest | A fix is awaiting validation by a pentester                                       |
| valid_fix    | Fixed            | The finding was fixed and validated by a pentester                                |
| wont_fix     | Accepted Risk    | The risk has been accepted. The finding will not be fixed                         |
| invalid      | Invalid          | The finding is invalid                                                            |
| duplicate    | Invalid          | The finding is invalid                                                            |
| out_of_scope | Invalid          | The finding is invalid                                                            |

## Get All Engagement Findings

```sh
curl -X GET "https://api.us.cobalt.io/engagement_findings" \
  -H "Accept: application/vnd.cobalt.v2+json" \
  -H "Authorization: Bearer YOUR-PERSONAL-API-TOKEN" \
  -H "X-Org-Token: YOUR-V2-ORGANIZATION-TOKEN"
```

> The above command returns JSON structured like this:

```json
{
  "pagination": {
    "next_page": "/engagement_findings?cursor=eyJwYWdlIjoyLCJzaXplIjoxMH0=",
    "prev_page": null
  },
  "data": [
    {
      "resource": {
        "finding_type": "digital_risk_assessment_finding",
        "id": "draf_5HPNLdMGN7kRV3Wjn3BDWv",
        "tag": "#DRA20540_6",
        "engagement_id": "dra_J9Edby7Qso4HzhgRzwktW4",
        "created_at": "2024-04-30T10:49:26.536Z",
        "title": "Title.",
        "description": "Description.",
        "affected_resource": "Resource.",
        "proof_of_concept": "Proof of concept.",
        "severity_description": "Severity description.",
        "suggested_fix": "Suggested fix.",
        "prerequisites": "Prerequisites.",
        "state": "new",
        "type_category": "",
        "impact": 1,
        "likelihood": 2,
        "attachments": []
      },
      "links": {
        "ui": {
          "url": "https://api.us.cobalt.io/links/eyJ0eXBlIjoiRU5HQUdFTUVOVCIsIm9yZ1NsdWciOiJtb2hyLXdhbGtlci05IiwicGVudGVzdFRhZyI6IiIsImZpbmRpbmdJZCI6IiIsImFzc2V0VGFnIjoiIiwiZW5nYWdlbWVudElkIjoiZHJhZl81SFBOTGRNR043a1JWM1dqbjNCRFd2IiwiZGFzdFRhcmdldElkIjoiIiwiZGFzdEZpbmRpbmdJZCI6IiIsImVuZ2FnZW1lbnRGaW5kaW5nSWQiOiIifQ=="
        }
      }
    },
    {
      "resource": {
        "finding_type": "secure_code_review_finding",
        "id": "scrf_6iz9f9PkNQe2P4PFXMP162",
        "tag": "#SCR26733_2",
        "engagement_id": "scr_HQFC6FaM8kZv17QBTe3rmR",
        "created_at": "2024-05-28T11:42:30.508Z",
        "title": "Title.",
        "description": "Description.",
        "affected_resource": "Affected resource.",
        "proof_of_concept": "Proof of concept.",
        "severity_description": "Severity descrption.",
        "suggested_fix": "Suggested fix.",
        "code_snippets": "Code snippets.",
        "state": "triaging",
        "target_asset_id": "as_A7EhhrnMZxSvfQPLqSFbE7",
        "type_category": "",
        "impact": 3,
        "likelihood": 3,
        "cvss_score": null,
        "attachments": []
      },
      "links": {
        "ui": {
          "url": "https://api.us.cobalt.io/links/eyJ0eXBlIjoiRU5HQUdFTUVOVCIsIm9yZ1NsdWciOiJtb2hyLXdhbGtlci05IiwicGVudGVzdFRhZyI6IiIsImZpbmRpbmdJZCI6IiIsImFzc2V0VGFnIjoiIiwiZW5nYWdlbWVudElkIjoic2NyZl82aXo5ZjlQa05RZTJQNFBGWE1QMTYyIiwiZGFzdFRhcmdldElkIjoiIiwiZGFzdEZpbmRpbmdJZCI6IiIsImVuZ2FnZW1lbnRGaW5kaW5nSWQiOiIifQ=="
        }
      }
    }
  ]
}
```

This endpoint retrieves a list of all engagement findings that belong to the organization specified in the `X-Org-Token`
header.

### HTTP Request

`GET https://api.us.cobalt.io/engagement_findings`

### URL Parameters

| Parameter | Default      | Description                                                                                                                                                                                                                                                                                                       |
|-----------|--------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `cursor`  | N/A          | Used for [pagination](./#pagination). Example: `https://api.us.cobalt.io/engagement_findings?cursor=eyJwYWdlIjoyLCJzaXplIjoxMH0=`                                                                                                                                                                                 |
| `sort`    | `created_at` | If specified, returns engagement findings sorted in ascending order by one of these properties: `created_at`, `impact`, `likelihood`, `severity`, `state`, or `updated_at`. To sort in descending order, use a `-` before the sort property. Example: `https://api.us.cobalt.io/engagement_findings?sort=-state`. |

### Response Fields {#engagement-finding-response-fields}

The fields that are returned depend on the engagement finding type.  This can be determined from the `finding_type`
field, which is common to all engagement finding types.

| Field                  | Engagement Finding Type(s)       | Description                                                                                                                              |
|------------------------|----------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|
| `affected_resource`    | All                              | Resource(s) impacted by the returned finding                                                                                             |
| `attachments`          | All                              | A list of finding attachments. Attachment download URLs are pre-authorized and will expire after 10 minutes                              |
| `code_snippets`        | Secure code review findings      | Code snippets demonstrating the issue with the returned finding                                                                          |
| `created_at`           | All                              | The timestamp when this finding was created.  Format: 2024-05-28T11:39:25.011Z                                                           |
| `cvss_score`           | Secure code review findings      | CVSS score for this finding                                                                                                              |
| `description`          | All                              | The description of the returned finding                                                                                                  |
| `engagement_id`        | All                              | The unique ID of the engagement this finding belongs to                                                                                  |
| `finding_type`         | All                              | The finding type. `digital_risk_assessment_finding` or `secure_code_review_finding`                                                      |
| `id`                   | All                              | A unique ID representing the finding                                                                                                     |
| `impact`               | All                              | If exploited, the potential impact of this finding. 0 (very low impact) - 5 (very high impact)                                           |
| `likelihood`           | All                              | How likely this finding is to be exploited. 0 (very unlikely) - 5 (very likely)                                                          |
| `prerequisites`        | Digital risk assessment findings | Conditions that must be fulfilled to successfully exploit the returned finding                                                           |
| `proof_of_concept`     | All                              | A proof of concept for the returned finding                                                                                              |
| `severity_description` | All                              | Description of the impact and likelihood of the returned finding                                                                         |
| `state`                | All                              | The state of the finding. `new`, `triaging`, `out_of_scope`, `invalid`, `duplicate`, `need_fix`, `check_fix`, `valid_fix`, or `wont_fix` |
| `suggested_fix`        | All                              | How to fix the returned finding                                                                                                          |
| `tag`                  | All                              | A human-friendly unique ID representing the finding                                                                                      |
| `target_asset_id`      | All                              | The unique ID of the asset impacted by the returned finding                                                                              |
| `title`                | All                              | The title of the returned finding                                                                                                        |
| `type_category`        | All                              | The general type category of the returned finding.  Example: XSS                                                                         |
| `links.ui.url`         | All                              | A link to redirect an authorized user to this finding in the Cobalt web application                                                      |

<aside class="notice">
Remember - you can only request engagement findings scoped to the organization specified in the <code>X-Org-Token</code>
header.
</aside>

## Get an Engagement Finding

```sh
curl -X GET "https://api.us.cobalt.io/engagement_findings/YOUR-ENGAGEMENT-FINDING-IDENTIFIER" \
  -H "Accept: application/vnd.cobalt.v2+json" \
  -H "Authorization: Bearer YOUR-PERSONAL-API-TOKEN" \
  -H "X-Org-Token: YOUR-V2-ORGANIZATION-TOKEN"
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "resource": {
      "finding_type": "secure_code_review_finding",
      "id": "scrf_CrmugETa3zTJWbu6ybRZMJ",
      "tag": "#SCR26733_1",
      "engagement_id": "scr_HQFC6FaM8kZv17QBTe3rmR",
      "created_at": "2024-05-28T11:39:25.011Z",
      "title": "Finding Title",
      "description": "Description.",
      "affected_resource": "Affected resource.",
      "proof_of_concept": "Proof of concept.",
      "severity_description": "Severity description.",
      "suggested_fix": "Suggested fix.",
      "code_snippets": "Code snippets.",
      "state": "need_fix",
      "target_asset_id": "as_4L4ZjKgfzP7VBwUmqCZmmL",
      "type_category": "Binary Planting",
      "impact": 3,
      "likelihood": 3,
      "cvss_score": "8.8 (AV:N/AC:L/PR:N/UI:R/S:C/C:H/I:H/A:H)",
      "attachments": [
        {
          "id": "at_LA5GcEL4HRitFGCHREqmzL",
          "file_name": "rainbow.jpeg",
          "download_url": "https://s3.amazonaws.com/acmecorp/uploads/attachment/file/12345/rainbow.jpeg?something=1"
        }
      ]
    },
    "links": {
      "ui": {
        "url": "https://api.us.cobalt.io/links/eyJ0eXBlIjoiRU5HQUdFTUVOVF9GSU5ESU5HIiwib3JnU2x1ZyI6Im1vaHItd2Fsa2VyLTkiLCJwZW50ZXN0VGFnIjoiIiwiZmluZGluZ0lkIjoiIiwiYXNzZXRUYWciOiIiLCJlbmdhZ2VtZW50SWQiOiJzY3JfSFFGQzZGYU04a1p2MTdRQlRlM3JtUiIsImRhc3RUYXJnZXRJZCI6IiIsImRhc3RGaW5kaW5nSWQiOiIiLCJlbmdhZ2VtZW50RmluZGluZ0lkIjoic2NyZl9Dcm11Z0VUYTN6VEpXYnU2eWJSWk1KIn0="
      }
    }
  }
}
```

This endpoint retrieves a specific engagement finding that belongs to the organization specified in the `X-Org-Token`
header.

### HTTP Request

`GET https://api.us.cobalt.io/engagement_findings/YOUR-ENGAGEMENT-FINDING-IDENTIFIER-HERE`

### Response Fields

For details about each response field, please refer to the [table above](/#engagement-finding-response-fields).

<aside class="notice">
Remember - you can only request an engagement finding scoped to the organization specified in the
<code>X-Org-Token</code> header.
</aside>
