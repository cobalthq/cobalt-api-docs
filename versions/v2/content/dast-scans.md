---
weight: 16
title: DAST Scans
---

# DAST Scans

## Get All DAST Scans

```sh
curl -X GET "https://api.us.cobalt.io/dast/scans" \
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
        "id": "dsc_GZgceqweJUNh6mjNuqsE4T",
        "target_id": "dt_GZgcehapJUNh6mjNuqsE4T",
        "status": "completed",
        "started_at": "2024-07-01T10:04:31.460Z",
        "completed_at": "2024-07-01T10:04:31.460Z"
      }
    }
  ]
}
```

This endpoint retrieves a list of all DAST scans that belong to the organization specified in the `X-Org-Token` header.

### HTTP Request

`GET https://api.us.cobalt.io/dast/scans`

### URL Parameters

| Parameter                      | Default | Description                                                                                                                                                                                                                                                                                                   |
|--------------------------------|---------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `cursor`                       | N/A     | Used for [pagination](./#pagination). Example: `https://api.us.cobalt.io/dast/scans?cursor=a1b2c3d4` |
| `limit`                        | `10`    | If specified, returns only a specified amount of scans. Example: `https://api.us.cobalt.io/dast/scans?limit=5` |
| `target`                       | N/A     | If specified, returns scans scoped to this target id. Example: `https://api.us.cobalt.io/dast/scans?target=dt_GZgcehapJUNh6mjNuqsE4T` |

### Response Fields

| Field           | Description                                                                         |
|-----------------|-------------------------------------------------------------------------------------|
| `id`      | A unique ID representing the DAST scan. Starts with `dsc_` |
| `target_id`    | A unique ID representing the DAST target. Starts with `dt_` |
| `status`     | Possible values: [`canceled`, `canceling`, `completed`, `completed_with_errors`, `failed`, `paused`, `pausing`, `queued`, `resuming`, `started`, `under_review`, `finishing_up`] |
| `started_at` | Date and time of when the scan started. |
| `completed_at` | Date and time of when the scan was completed. |

## Get a DAST Scan

```sh
curl -X GET "https://api.us.cobalt.io/dast/scans/YOUR-DAST-SCAN-IDENTIFIER" \
  -H "Accept: application/vnd.cobalt.v2+json" \
  -H "Authorization: Bearer YOUR-PERSONAL-API-TOKEN" \
  -H "X-Org-Token: YOUR-V2-ORGANIZATION-TOKEN"
```

> The above command returns JSON structured like this:

```json
{
  "resource": {
    "id": "dsc_GZgceqweJUNh6mjNuqsE4T",
    "target_id": "dt_GZgcehapJUNh6mjNuqsE4T",
    "status": "completed",
    "started_at": "2024-07-01T10:19:11.160Z",
    "completed_at": "2024-07-01T10:19:11.160Z"
  }
}
```

This endpoint retrieves a specific DAST Scan that belongs to the organization specified in the `X-Org-Token` header.

### HTTP Request

`GET https://api.us.cobalt.io/dast/scans/YOUR-DAST-SCAN-IDENTIFIER`

### Response Fields

| Field           | Description                                                                         |
|-----------------|-------------------------------------------------------------------------------------|
| `id`      | A unique ID representing the DAST scan. Starts with `dsc_` |
| `target_id`    | A unique ID representing the DAST target. Starts with `dt_` |
| `status`     | Possible values: [`canceled`, `canceling`, `completed`, `completed_with_errors`, `failed`, `paused`, `pausing`, `queued`, `resuming`, `started`, `under_review`, `finishing_up`] |
| `started_at` | Date and time of when the scan started. |
| `completed_at` | Date and time of when the scan was completed. |

## Create a DAST Scan

```sh
curl -X POST "https://api.us.cobalt.io/dast/scans/targets/YOUR-DAST-TARGET-IDENTIFIER/scans" \
  -H "Accept: application/vnd.cobalt.v2+json" \
  -H "Authorization: Bearer YOUR-PERSONAL-API-TOKEN" \
  -H "X-Org-Token: YOUR-V2-ORGANIZATION-TOKEN"
```

> The above command returns JSON structured like this:

```json
{
  "resource": {
    "id": "dsc_GZgceqweJUNh6mjNuqsE4T",
    "target_id": "dt_GZgcehapJUNh6mjNuqsE4T",
    "status": "queued",
    "started_at": "2024-07-01T10:19:11.160Z",
    "completed_at": "2024-07-01T10:19:11.160Z"
  }
}
```

This endpoint triggers a new DAST scan on the specified target. The scan will start in the `queued` state and progress to `completed` or `failed`

### HTTP Request

`POST https://api.us.cobalt.io/dast/scans/targets/YOUR-DAST-TARGET-IDENTIFIER/scans`

### URL Parameters

| Parameter                      | Description                                            |
|--------------------------------|--------------------------------------------------------|
| `YOUR-DAST-TARGET-IDENTIFIER`  | A unique ID representing the target. Starts with `dt_` |

### Response Fields

| Field           | Description                                                                         |
|-----------------|-------------------------------------------------------------------------------------|
| `id`      | A unique ID representing the DAST scan. Starts with `dsc_` |
| `target_id`    | A unique ID representing the DAST target. Starts with `dt_` |
| `status`     | Possible values: [`canceled`, `canceling`, `completed`, `completed_with_errors`, `failed`, `paused`, `pausing`, `queued`, `resuming`, `started`, `under_review`, `finishing_up`] |
| `started_at` | Date and time of when the scan started. |
| `completed_at` | Date and time of when the scan was completed. |
