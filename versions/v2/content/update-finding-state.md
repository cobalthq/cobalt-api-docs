---
weight: 9
title: Update Finding State
---

## View Available Finding States

```sh
curl -X GET "https://api.us.cobalt.io/findings/YOUR-FINDING-ID/possible_states" \
  -H "Accept: application/vnd.cobalt.v2+json" \
  -H "Authorization: Bearer YOUR-PERSONAL-API-TOKEN" \
  -H "X-Org-Token: YOUR-V2-ORGANIZATION-TOKEN"
```

> The above command returns JSON structured like this:

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

This endpoint retrieves the current state of a finding as well as possible next states.

### HTTP Request

`GET https://api.us.cobalt.io/findings/YOUR-FINDING-ID/possible_states`

### URL Parameters

| Parameter         | Description                                             |
|-------------------|---------------------------------------------------------|
| `YOUR-FINDING-ID` | A unique ID representing the finding. Starts with `vl_` |

### Response Fields

| Field             | Description                                                                                             |
|-------------------|---------------------------------------------------------------------------------------------------------|
| `current_state`   | The current state of the finding.                                                                       |
| `possible_states` | A list of states that the finding can be transitioned to. See [Finding States Documentation](./#states) |

## Update Finding State

```sh
curl -X PATCH "https://api.us.cobalt.io/findings/YOUR-FINDING-ID" \
  -H "Accept: application/vnd.cobalt.v2+json" \
  -H "Content-Type: application/vnd.cobalt.v2+json" \
  -H "Idempotency-Key: A-UNIQUE-IDENTIFIER-TO-PREVENT-UNINTENTIONAL-DUPLICATION" \
  -H "Authorization: Bearer YOUR-PERSONAL-API-TOKEN" \
  -H "X-Org-Token: YOUR-V2-ORGANIZATION-TOKEN" \
  -d '{"state":"triaging"}'
```

> If successful, this command returns `204`.

This endpoint updates the current state of a finding.

### HTTP Request

`PATCH https://api.us.cobalt.io/findings/YOUR-FINDING-ID`

### URL Parameters

| Parameter         | Description                                             |
|-------------------|---------------------------------------------------------|
| `YOUR-FINDING-ID` | A unique ID representing the finding. Starts with `vl_` |

### Body

| Field   | Description                                                                               |
|---------|-------------------------------------------------------------------------------------------|
| `state` | The desired next state of the finding. Should be one of the possible [states](./#states). |
