---
weight: 17
title: DAST Findings
---

# DAST Findings

## Get All DAST Findings

```sh
curl -X GET "https://api.us.cobalt.io/dast/findings" \
  -H "Accept: application/vnd.cobalt.v2+json" \
  -H "Authorization: Bearer YOUR-PERSONAL-API-TOKEN" \
  -H "X-Org-Token: YOUR-V2-ORGANIZATION-TOKEN"
```

> The above command returns JSON structured like this:

```json
{
  "pagination": {
    "next_page": "/resource?cursor=123asdzxc",
    "prev_page": "/resource?cursor=123asdzxc"
  },
  "data": [
    {
      "resource": {
        "id": "dfi_2pF7XE2nJyP3i8ComjVXj3",
        "target_id": "dt_GZgcehapJUNh6mjNuqsE4T",
        "scan_ids": [
          "dsc_GZgceqweJUNh6mjNuqsE4T"
        ],
        "title": "string",
        "last_found_at": "2024-07-01T10:39:31.919Z",
        "severity": "string",
        "state": "string",
        "affected_url": "string",
        "description": "string",
        "proof_of_concept": "string",
        "suggested_fix": "string",
        "http_exchanges": [
          {
            "request": "string",
            "response": "string"
          }
        ]
      }
    }
  ]
}
```

This endpoint retrieves a list of all DAST findings that belong to the organization specified in the `X-Org-Token` header.

### HTTP Request

`GET https://api.us.cobalt.io/dast/findings`

### URL Parameters

| Parameter | Default | Description |
|-------------|---------|-----------------------|
| `cursor`   | N/A     | Used for [pagination](./#pagination). Example: `https://api.us.cobalt.io/dast/findings?cursor=a1b2c3d4` |
| `limit`    | `10`    | If specified, returns only a specified amount of findings. Example: `https://api.us.cobalt.io/dast/findings?limit=5` |
| `target`   | N/A     | If specified, returns findings scoped to this target id. Example: `https://api.us.cobalt.io/dast/findings?target=dt_GZgcehapJUNh6mjNuqsE4T` |
| `scan`     | N/A     | If specified, returns findings scoped to this scan id. Example: `https://api.us.cobalt.io/dast/findings?scan=dsc_GZgcehapJUNh6mjNuqsE4T` |

### Response Fields

See [Finding response fields](#finding-response-fields)

## Get a DAST Finding

```sh
curl -X GET "https://api.us.cobalt.io/dast/findings/YOUR-DAST-FINDING-IDENTIFIER" \
  -H "Accept: application/vnd.cobalt.v2+json" \
  -H "Authorization: Bearer YOUR-PERSONAL-API-TOKEN" \
  -H "X-Org-Token: YOUR-V2-ORGANIZATION-TOKEN"
```

> The above command returns JSON structured like this:

```json
{
  "resource": {
    "id": "dfi_2pF7XE2nJyP3i8ComjVXj3",
    "target_id": "dt_GZgcehapJUNh6mjNuqsE4T",
    "scan_ids": [
      "dsc_GZgceqweJUNh6mjNuqsE4T"
    ],
    "title": "string",
    "last_found_at": "2024-07-01T10:56:34.997Z",
    "severity": "string",
    "state": "string",
    "affected_url": "string",
    "description": "string",
    "proof_of_concept": "string",
    "suggested_fix": "string",
    "http_exchanges": [
      {
        "request": "string",
        "response": "string"
      }
    ]
  }
}
```

This endpoint retrieves a specific DAST finding that belongs to the organization specified in the `X-Org-Token` header.

### HTTP Request

`GET https://api.us.cobalt.io/dast/findings/YOUR-DAST-FINDING-IDENTIFIER`

### URL Parameters

| Parameter                      | Description                                              |
|--------------------------------|----------------------------------------------------------|
| `YOUR-DAST-FINDING-IDENTIFIER` | A unique ID representing the finding. Starts with `dfi_` |

### Finding Response Fields

| Field           | Description                                                                         |
|-----------------|-------------------------------------------------------------------------------------|
| `id`                | A unique ID representing the DAST finding. Starts with `dfi_` |
| `target_id`         | A unique ID representing the DAST target. Starts with `dt_` |
| `scan_ids`          | An array of unique ID representing the scans that originated the vulnerability finding. Starts with `dsc_` |
| `title`             | Name of the vulnerability |
| `last_found_at`     | Date and time of when the vulnerability was last found, in ISO 8601 UTC format. |
| `severity`          | Severity of the vulnerability finding: `10` is low. `20` is medium. `30` is high. |
| `state`             | State of the vulnerability finding: [`invalid`, `need_fix`, `wont_fix`, `valid_fix`, `check_fix`] |
| `affected_url`      | URL affected by the found vulnerability |
| `description`       | Description of the vulnerability. |
| `proof_of_concept`  | Evidence of the vulnerability finding. |
| `suggested_fix`     | Description of how to fix the vulnerability. |
| `http_exchanges`    | Pairs of `request` and `response` of the vulnerability finding. |

## Retest DAST finding

```sh
curl -X POST "https://api.us.cobalt.io/dast/findings/YOUR-DAST-FINDING-IDENTIFIER/retest" \
  -H "Accept: application/vnd.cobalt.v2+json" \
  -H "Authorization: Bearer YOUR-PERSONAL-API-TOKEN" \
  -H "X-Org-Token: YOUR-V2-ORGANIZATION-TOKEN"
```

> The above command returns no data and a `204` response code when successful.

This endpoint runs a short scan to determine if the finding can still be detected. The state
of the finding will change automatically once the retest finishes. Because DAST findings
are of an automated nature, retesting and passing the scan is the only way to mark it as fixed.

### HTTP Request

`POST https://api.us.cobalt.io/dast/findings/YOUR-DAST-FINDING-IDENTIFIER/retest`

### URL Parameters

| Parameter                      | Description                                              |
|--------------------------------|----------------------------------------------------------|
| `YOUR-DAST-FINDING-IDENTIFIER` | A unique ID representing the finding. Starts with `dfi_` |

## Update Finding State

```sh
curl -X PATCH "https://api.us.cobalt.io/dast/findings/YOUR-DAST-FINDING-IDENTIFIER" \
  -H "Accept: application/vnd.cobalt.v2+json" \
  -H "Content-Type: application/vnd.cobalt.v2+json" \
  -H "Authorization: Bearer YOUR-PERSONAL-API-TOKEN" \
  -H "X-Org-Token: YOUR-V2-ORGANIZATION-TOKEN" \
  -d '{"state":"need_fix"}'
```

> If successful, this command returns `200` and the updated finding

This endpoint updates the current state of a DAST finding. Note that changing the state to `fixed` or `check_fix` is not
possible with this endpoint. You have to use the [retest endpoint](#retest-dast-finding) for that.

### HTTP Request

`PATCH https://api.us.cobalt.io/dast/findings/YOUR-DAST-FINDING-IDENTIFIER`

### URL Parameters

| Parameter                      | Description                                              |
|--------------------------------|----------------------------------------------------------|
| `YOUR-DAST-FINDING-IDENTIFIER` | A unique ID representing the finding. Starts with `dfi_` |

### Body

| Field   | Description                                                                               |
|---------|-------------------------------------------------------------------------------------------|
| `state` | The desired next state of the finding. Should be one of [`invalid`, `wont_fix`, `need_fix`] |

### Response fields

See [Finding response fields](#finding-response-fields)
