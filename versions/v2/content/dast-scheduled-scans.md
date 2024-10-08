---
weight: 16
title: DAST Scheduled Scans
---

# DAST Scheduled Scans

## Create a scheduled DAST Scan

```sh
curl -X POST "https://api.us.cobalt.io/dast/targets/YOUR-DAST-TARGET-IDENTIFIER/scheduled_scans" \
  -H "Accept: application/vnd.cobalt.v2+json" \
  -H "Content-Type: application/vnd.cobalt.v2+json" \
  -H "Authorization: Bearer YOUR-PERSONAL-API-TOKEN" \
  -H "X-Org-Token: YOUR-V2-ORGANIZATION-TOKEN" \
  --data '{
            "date_time": "2024-07-01T10:19:11.160Z",
            "recurrence": "WEEKLY"
          }'
```

> The above command returns JSON structured like this:

```json
{
  "resource": {
    "id": "dsc_GZgceqweJUNh6mjNuqsE4T",
    "target_id": "dt_GZgcehapJUNh6mjNuqsE4T",
    "date_time": "2024-07-01T10:19:11.160Z",
    "recurrence": "WEEKLY"
  }
}
```

This endpoint creates a new scheduled DAST scan on the specified target. The scan will start when the `date_time` is reached
or the next time the recurrence would happen.

### HTTP Request

`POST https://api.us.cobalt.io/dast/scans/targets/YOUR-DAST-TARGET-IDENTIFIER/scheduled_scans`

### Body

| Field        | Description                                                                                                                    |
|--------------|--------------------------------------------------------------------------------------------------------------------------------|
| `recurrence` | Optional; if present, the scan will be triggered every certain time period. Available values: `WEEKLY`, `MONTHLY`, `QUARTERLY` |
| `date_time`  | Date and time of when the scan will run                                                                                        |

### URL Parameters

| Parameter                      | Description                                            |
|--------------------------------|--------------------------------------------------------|
| `YOUR-DAST-TARGET-IDENTIFIER`  | A unique ID representing the target. Starts with `dt_` |

### Response Fields

| Field           | Description                                                                         |
|-----------------|-------------------------------------------------------------------------------------|
| `id`      | A unique ID representing the DAST scan. Starts with `dsc_` |
| `target_id`    | A unique ID representing the DAST target. Starts with `dt_` |
| `date_time` | Date and time of when the scan will run |
| `recurrence` | How often will the scan run. Possible vaules: `WEEKLY`, `MONTHLY`, `QUARTERLY`. Nullable (no recurrence)  |
