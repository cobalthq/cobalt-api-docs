---
weight: 9
title: Update Finding State
---

## View Available Finding States

```sh
curl -X GET "https://api.cobalt.io/findings/YOUR-FINDING-ID/possible_states" \
  -H "Accept: application/vnd.cobalt.v2+json" \
  -H "Authorization: Bearer YOUR-PERSONAL-API-TOKEN" \
  -H "X-Org-Token: YOUR-V2-ORGANIZATION-TOKEN"
```

> Response Sample

```json
{
  "resource": {
    "current_state": "invalid",
    "possible_states": [
      "triaging",
      "need_fix",
      "duplicate",
      "out_of_scope"
    ]
  }
}
```

Returns the current state of a finding and possible next states.

{{% add-org-token %}}

### HTTP Request

`GET https://api.cobalt.io/findings/YOUR-FINDING-ID/possible_states`

### Query Parameters

| Name         | Description                                                  |
|-------------------|--------------------------------------------------------------|
| `YOUR-FINDING-ID` | {{% finding-id %}} Starts with `vl_`. |

### Response Parameters

| Name             | Description                                               |
|-------------------|-----------------------------------------------------------|
| `current_state`   | The current state of the finding. See possible values in [Finding States](./#finding-states). |
| `possible_states` | A list of states that the finding can be transitioned to. |

## Update Finding State

```sh
curl -X PATCH "https://api.cobalt.io/findings/YOUR-FINDING-ID" \
  -H "Accept: application/vnd.cobalt.v2+json" \
  -H 'Content-Type: application/vnd.cobalt.v2+json' \
  -H "Authorization: Bearer YOUR-PERSONAL-API-TOKEN" \
  -H "X-Org-Token: YOUR-V2-ORGANIZATION-TOKEN" \
  -d '{"state":"triaging"}'
```

> {{% 204-code %}}

Updates the current state of a finding.

{{% add-org-token %}}

### HTTP Request

`PATCH https://api.cobalt.io/findings/YOUR-FINDING-ID`

### Query Parameters

| Name         | Description                                                  |
|-------------------|--------------------------------------------------------------|
| `YOUR-FINDING-ID` | {{% finding-id %}} Starts with `vl_`. |

### Request Body

| Name   | Description                                                                  |
|---------|------------------------------------------------------------------------------|
| `state` | The state to transition the finding to. Must be one of the possible states. [Get available finding states](./#view-available-finding-states), and find `possible_states` in the response. |
