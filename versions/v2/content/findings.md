---
weight: 8
title: Findings
---

# Findings

## Get All Findings

```sh
curl -X GET "https://api.us.cobalt.io/findings" \
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
        "id": "vl_3sP2RCWWUajc3oRXmbQ4j9",
        "tag": "#PT3334_37",
        "title": "XSS vulnerability",
        "description": "Cross-Site Scripting (XSS) attacks are a type of injection, in which malicious scripts...",
        "type_category": "Cross-Site Scripting (XSS)",
        "labels": [
          {
            "name": "Your label"
          }
        ],
        "impact": 5,
        "likelihood": 4,
        "severity": "high",
        "affected_targets": [
          "https://example.com",
          "192.168.1.1"
        ],
        "proof_of_concept": "Here you can see...",
        "severity_justification": "The vulnerability can cause a lot of damage",
        "suggested_fix": "Ensure this...",
        "prerequisites": "Credentials are needed",
        "pentest_id": "pt_PEtv4dqnwGV2efZhLw3BM5",
        "http_request": "HTTP GET / ...",
        "asset_id": "as_HcChCMueiPQQgvckmZtRSd",
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
        "state": "check_fix",
        "created_at": "2022-09-26T18:35:18.759Z",
        "updated_at": "2022-09-26T18:36:57.462Z",
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
          "url": "https://api.us.cobalt.io/links/eyJ0eXBlIjoic29tZXRoaW5nIiwib3JnU2x1ZyI6ImNvYmFsdCIsInBlbnRlc3RUYWciOiJz="
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

This endpoint retrieves a list of all pentest findings that belong to the organization specified in the `X-Org-Token`
header, filterable by `pentest_id` or `asset_id`. The `log` array presents a history of each finding and corresponding
timestamp.

### Calculations

We follow the standard risk model described by OWASP, where:

`Risk = Impact * Likelihood`

Cobalt Risk Input Fields:

- `impact`: 1, 2, 3, 4, or 5
- `likelihood`: 1, 2, 3, 4, or 5

Cobalt Risk Classification (`severity`, a.k.a. `criticality`):

| Category        | Score | Description                                                                                                                                                     |
|-----------------|-------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `critical`      | 25    | Includes vulnerabilities that require immediate attention.                                                                                                      |
| `high`          | 16-24 | Impacts the security of your application/platform/hardware, including supported systems. Includes high probability vulnerabilities with a high business impact. |
| `medium`        | 5-15  | Includes vulnerabilities that are: medium risk, medium impact; low risk, high impact; high risk, low impact.                                                    |
| `low`           | 2-4   | Specifies common vulnerabilities with minimal impact.                                                                                                           |
| `informational` | 1     | Notes vulnerabilities of minimal risk to your business.                                                                                                         |

### HTTP Request

`GET https://api.us.cobalt.io/findings`

### URL Parameters

| Parameter                         | Default    | Description                                                                                                                                                                                                                                                                                                                                     |
|-----------------------------------|------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `cursor`                          | N/A        | Used for [pagination](./#pagination). Example: `https://api.us.cobalt.io/findings?cursor=a1b2c3d4`                                                                                                                                                                                                                                              |
| `limit`                           | `10`       | If specified, returns only a specified amount of findings. Example: `https://api.us.cobalt.io/findings?limit=5`                                                                                                                                                                                                                                 |
| `pentest`                         | N/A        | If specified, returns findings scoped to this pentest id. Example: `https://api.us.cobalt.io/findings?pentest=pt_PEtv4dqnwGV2efZhLw3BM5`                                                                                                                                                                                                        |
| `asset`                           | N/A        | If specified, returns findings scoped to this asset id. Example: `https://api.us.cobalt.io/findings?asset=as_HcChCMueiPQQgvckmZtRSd`                                                                                                                                                                                                            |
| `state`                           | N/A        | If specified, returns findings that match `state`. See Response Fields below for example `state` values. Example: `https://api.us.cobalt.io/findings?state=check_fix`. Returns an empty list if no findings match the `state` filter.                                                                                                           |
| `severity`                        | N/A        | If specified, returns findings that match `severity`. See Response Fields below for example `severity` values. Example: `https://api.us.cobalt.io/findings?severity=medium`. Returns an empty list if no findings match the `severity` filter.                                                                                                  |
| `labels_contains_all[]`           | N/A        | If specified, returns findings that contain all specified labels. This query parameter can be specified multiple times. Returns an empty list if no matches are found. Example: `https://api.us.cobalt.io/findings?labels_contains_all[]=Awaiting Feedback&labels_contains_all[]=Retest Blocked`                                                |
| `sort`                            | N/A        | If specified, returns findings sorted by one of the chosen parameters: `severity`, `impact`, `state`, `created_at` and `updated_at`. When defined, findings are sorted in ascending order by the sort parameter. To sort in descending order, use a `-` before the sort parameter. Example: `https://api.us.cobalt.io/findings?sort=-severity`. |
| `created_at_lte`                  | N/A        | If specified, returns findings where the created_at timestamp is less than or equal to the input timestamp. ISO8601 is the supported input timestamp format. Returns an empty list if no findings match the filter. Example: `https://api.us.cobalt.io/findings?created_at_lte=2020-02-20T15:28:10.335Z`                                        |
| `created_at_gte`                  | N/A        | If specified, returns findings where the created_at timestamp is greater than or equal to the input timestamp. ISO8601 is the supported input timestamp format. Returns an empty list if no findings match the filter. Example: `https://api.us.cobalt.io/findings?created_at_gte=2020-02-20T15:28:10.335Z`                                     |
| `updated_at_lte`                  | N/A        | If specified, returns findings where the updated_at timestamp is less than or equal to the input timestamp. ISO8601 is the supported input timestamp format. Returns an empty list if no findings match the filter. Example: `https://api.us.cobalt.io/findings?updated_at_lte=2020-02-20T15:28:10.335Z`                                        |
| `updated_at_gte`                  | N/A        | If specified, returns findings where the updated_at timestamp is greater than or equal to the input timestamp. ISO8601 is the supported input timestamp format. Returns an empty list if no findings match the filter. Example: `https://api.us.cobalt.io/findings?updated_at_gte=2020-02-20T15:28:10.335Z`                                     |
| `image_attachments_render_format` | `markdown` | If specified, returns image attachments with the specified render format. Supported values are `markdown` and `token`. Example: `https://api.us.cobalt.io/findings?image_attachments_render_format=token`. See the Image Attachments section for more information                                                                               | 

### Response Fields

| Field                    | Enum Types                                                                                                                     |
|--------------------------|--------------------------------------------------------------------------------------------------------------------------------|
| `log`                    | `created`, `impact_changed`, `likelihood_changed`, `state_changed`                                                             |
| `severity`               | `null`, `low`, `medium`, `high`  (aka `criticality`. will be null if likelihood/impact have not yet been set by the pentester) |
| `severity_justification` | Optional; The justification for the severity rating                                                                            |
| `prerequisites`          | Optional; The prerequisites required for reproducing the vulnerability                                                         |
| `http_request`           | Optional; An example HTTP request for reproducing the vulnerability                                                            |
| `state`                  | `new`, `triaging`, `need_fix`, `wont_fix`, `valid_fix`, `check_fix`, `invalid`, `carried_over`                                 |
| `type_category`          | XSS, SQLi, ... (about 30 more via the Cobalt Taxonomy)                                                                         |
| `attachments`            | A list of finding attachments. Attachment download URLs are pre-authorized and will expire after 10 minutes.                   |
| `links.ui.url`           | A link to redirect an authorized user to this finding in the Cobalt web application                                            |

### Image Attachments

Several finding fields support image attachments. By default, these attachments will be rendered in our response JSON as markdown. Example: `![screenshot.png](https://api.us.cobalt.io/v1/attachments/att_xxxxxxx/preview)`.
This format is not useful for users that want to programmatically download the attachments and associate them to a certain position in the finding response.
For this use case, we support a `token` format which will render the attachment as a token that can be used to download the attachment. Example: `<CobaltImageAttachment at_KYKDAhZPXuQ4BW23g8i9QN>`.
The token format allows users to use a technology such as RegEx to search the finding response fields for image attachments and extract the image attachment IDs. Within the example token, `at_KYKDAhZPXuQ4BW23g8i9QN` is the attachment ID.
Using the attachment ID, users can find the full attachment information by searching the `attachments` array in the finding response for an attachment object with a matching ID.
The attachment object contains a `download_url` field that can be used to download the attachment.

### State

- `new`: The finding has been created but not yet triaged.
- `triaging`: The finding is being evaluated.
- `need_fix`: The finding was deemed valid and a fix either is being developed or will be developed in the future.
- `wont_fix`: The finding was deemed valid but immaterial or meaningless and will not be addressed.
- `check_fix`: A fix has been applied and now is awaiting validation by the pentester.
- `invalid`: The finding was rejected as not being a true vulnerability.
- `carried_over`: The finding was carried over from a previous pentest.

<aside class="notice">
Remember - you can only request findings scoped to the organization specified in the <code>X-Org-Token</code> header.
</aside>

## Get a Finding

```sh
curl -X GET "https://api.us.cobalt.io/findings/YOUR-FINDING-IDENTIFIER" \
  -H "Accept: application/vnd.cobalt.v2+json" \
  -H "Authorization: Bearer YOUR-PERSONAL-API-TOKEN" \
  -H "X-Org-Token: YOUR-V2-ORGANIZATION-TOKEN"
```

> The above command returns JSON structured like this:

```json
{
  "resource": {
    "id": "vl_3sP2RCWWUajc3oRXmbQ4j9",
    "tag": "#PT5940",
    "title": "XSS vulnerability",
    "description": "Cross-Site Scripting (XSS) attacks are a type of injection, in which malicious scripts...",
    "type_category": "Cross-Site Scripting (XSS)",
    "labels": [
      {
        "name": "Your label"
      }
    ],
    "impact": 5,
    "likelihood": 4,
    "severity": "high",
    "affected_targets": [
      "https://example.com",
      "192.168.1.1"
    ],
    "proof_of_concept": "Here you can see...",
    "severity_justification": "The vulnerability can cause a lot of damage",
    "suggested_fix": "Ensure this...",
    "prerequisites": "Credentials are needed",
    "pentest_id": "pt_PEtv4dqnwGV2efZhLw3BM5",
    "http_request": "HTTP GET / ...",
    "asset_id": "as_HcChCMueiPQQgvckmZtRSd",
    "log": [
      {
        "action": "created",
        "timestamp": "2021-09-22T18:43:01.677Z"
      }
    ],
    "state": "new",
    "created_at": "2022-09-26T18:35:18.759Z",
    "updated_at": "2022-09-26T18:36:57.462Z",
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
      "url": "https://api.us.cobalt.io/links/eyJ0eXBlIjoic29tZXRoaW5nIiwib3JnU2x1ZyI6ImNvYmFsdCIsInBlbnRlc3RUYWciOiJz="
    }
  }
}
```

This endpoint retrieves a specific finding that belong to the organization specified in the `X-Org-Token` header.

### HTTP Request

`GET https://api.us.cobalt.io/findings/YOUR-FINDING-IDENTIFIER`

### Response Fields

| Field                    | Enum Types                                                                                                            |
|--------------------------|-----------------------------------------------------------------------------------------------------------------------|
| `log`                    | created, impact_changed, likelihood_changed, state_changed                                                            |
| `severity`               | null, low, medium, high (aka `criticality`. will be null if likelihood/impact have not yet been set by the pentester) |
| `severity_justification` | Optional; The justification for the severity rating                                                                   |
| `prerequisites`          | Optional; The prerequisites required for reproducing the vulnerability                                                |
| `http_request`           | Optional; An example HTTP request for reproducing the vulnerability                                                   |
| `state`                  | new, triaging, need_fix, wont_fix, valid_fix, check_fix, invalid, carried_over                                        |
| `type_category`          | XSS, SQLi, ... (about 30 more via the Cobalt Taxonomy)                                                                |
| `attachments`            | A list of finding attachments. Attachment download URLs are pre-authorized and will expire after 10 minutes.          |
| `url`                    | The links.ui.url will redirect an authorized user to this finding in the Cobalt platform                              |

### State

- `new`: The finding has been created but not yet triaged.
- `triaging`: The finding is being evaluated.
- `need_fix`: The finding was deemed valid and a fix either is being developed or will be developed in the future.
- `wont_fix`: The finding was deemed valid but immaterial or meaningless and will not be addressed.
- `check_fix`: A fix has been applied and now is awaiting validation by the pentester.
- `invalid`: The finding was rejected as not being a true vulnerability.
- `carried_over`: The finding was carried over from a previous pentest.

<aside class="notice">
Remember - you can only request a finding scoped to the organization specified in the <code>X-Org-Token</code> header.
</aside>
