---
weight: 9
title: Update Finding State
---

## Update Finding State

### API V1

This operation is not supported by `v1` of the API.

### API V2

#### View Available States

```sh
curl -X GET "https://api.cobalt.io/findings/vl_FINDING_ID/possible_states" \
  -H "accept: application/vnd.cobalt.v2+json" \
  -H "Authorization: Bearer your-personal-api-token-here" \
  -H "X-Org-Token: your-org-token-here"
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

#### Update State

```sh
curl -X PATCH "https://api.cobalt.io/findings/vl_FINDING_ID" \
  -H "accept: application/vnd.cobalt.v2+json" \
  -H "Authorization: Bearer your-personal-api-token-here" \
  -H "X-Org-Token: your-org-token-here" \
  -d '{"state":"triaging"}'
```

> If successful, this command returns `204`.
