---
weight: 18
title: External Ticket References
---

# External Ticket References

## Search External Ticket References

```sh
curl --location 'https://api.us.cobalt.io/external_ticket_references/search' \
  -H "Accept: application/vnd.cobalt.v2+json" \
  -H "Authorization: Bearer YOUR-PERSONAL-API-TOKEN" \
  -H "X-Org-Token: YOUR-V2-ORGANIZATION-TOKEN"
  --data '{}'
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "resource": {
        "id": "efr_NgGSgvKVGLeTpVHAiGWkMG",
        "title": "6",
        "reference_type": "azure_devops_boards",
        "ticketing_system": "azure_devops_boards",
        "external_url": "https://dev.azure.com/my-project/test/_workitems/edit/6",
        "external_id": "my-project-test-6",
        "finding_id": "vl_4C5HhhycuKM6BYY72PpftM"
      }
    },
    {
      "resource": {
        "id": "efr_8wDddLH13BoMoyvEtMEvPX",
        "title": "123",
        "reference_type": "github",
        "ticketing_system": "github",
        "external_url": "https://github.com/my-org/my-project/issue/123",
        "external_id": "my-org-my-project-123",
        "finding_id": "vl_JTovzf8AW1afCRpKJejse3"
      }
    },
    {
      "resource": {
        "id": "efr_2qkKUC1PGDPR7KhvixTsXW",
        "title": "TEST-36",
        "reference_type": "jira",
        "ticketing_system": "jira",
        "external_url": "https://my-project.atlassian.net/browse/TEST-36",
        "external_id": "10213",
        "finding_id": "dfi_2bZrrKE3Hay7oLrbNUponW"
      }
    }
  ]
}
```

This endpoint retrieves a list of all external ticket references that belong to the organization specified in the `X-Org-Token`
header.

If you want to filter the search results based on a subset of findings, you can use the `findings` property in the
request body.

```sh
curl --location 'https://api.us.cobalt.io/external_ticket_references/search' \
  -H "Accept: application/vnd.cobalt.v2+json" \
  -H "Authorization: Bearer YOUR-PERSONAL-API-TOKEN" \
  -H "X-Org-Token: YOUR-V2-ORGANIZATION-TOKEN"
  --data '{"findings":[{"id":"vl_JTovzf8AW1afCRpKJejse3"},{"id":"dfi_2bZrrKE3Hay7oLrbNUponW"}]}'
```

### HTTP Request

`POST https://api.us.cobalt.io/external_ticket_references/search`

### Request Body

| Field      | Description                                                                                                                                     |
| ---------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| `findings` | An array of finding ID `object`s to filter the search. For example, `[{"id":"vl_JTovzf8AW1afCRpKJejse3"},{"id":"dfi_2bZrrKE3Hay7oLrbNUponW"}]`. |

<aside class="notice">
Remember - if the <code>findings</code> property is defined in the search request body, but is empty, the search result
will always be empty.
</aside>

## Create an External Ticket Reference

```sh
curl --location 'https://api.us.cobalt.io/external_ticket_references' \
  -H "Accept: application/vnd.cobalt.v2+json" \
  -H "Authorization: Bearer YOUR-PERSONAL-API-TOKEN" \
  -H "X-Org-Token: YOUR-V2-ORGANIZATION-TOKEN"
  --data '{"title":"TEST-37","ticketing_system":"jira","external_url":"https://my-project.atlassian.net/browse/TEST-37","external_id":"10214","finding_id":"vl_JTovzf8AW1afCRpKJejse3"}'
```

> The above command returns the created external ticket reference and a `201` response code when successful.

```json
{
  "resource": {
    "id": "efr_9ekpSErugPH8zst2pBcjPo",
    "title": "TEST-37",
    "ticketing_system": "jira",
    "external_url": "https://my-project.atlassian.net/browse/TEST-37",
    "external_id": "10214",
    "finding_id": "vl_JTovzf8AW1afCRpKJejse3"
  }
}
```

This endpoint creates the external ticket reference, and on a successful request, it will return a `201` response code
along with the created external ticket reference information.

### HTTP Request

`POST https://api.us.cobalt.io/external_ticket_references`

### Request Body

| Field              | Description                                                                   |
| ------------------ | ----------------------------------------------------------------------------- |
| `title`            | A short descriptive title of the external ticket. For example, the ticket ID. |
| `ticketing_system` | One of the supported [ticking system](#ticketing-system).                     |
| `external_url`     | The URL of the external ticket.                                               |
| `external_id`      | An arbitrary external identifier for the ticket reference.                    |
| `finding_id`       | The Cobalt ID of the finding this external ticket belongs to.                 |

### Response

You get a `201` response code for a successful request.

| Field              | Description                                                                   |
| ------------------ | ----------------------------------------------------------------------------- |
| `id`               | A unique ID representing the external ticket reference. Starts with `efr_`    |
| `title`            | A short descriptive title of the external ticket. For example, the ticket ID. |
| `ticketing_system` | One of the supported [ticking system](#ticketing-system).                     |
| `external_url`     | The URL of the external ticket.                                               |
| `external_id`      | An arbitrary external identifier for the ticket reference.                    |
| `finding_id`       | The Cobalt ID of the finding this external ticket belongs to.                 |

## Delete an External Ticket Reference

```sh
curl -X DELETE 'https://api.us.cobalt.io/external_ticket_references/YOUR-EXTERNAL-TICKET-REFERENCE-IDENTIFIER' \
  -H 'Accept: application/vnd.cobalt.v2+json' \
  -H 'Authorization: Bearer YOUR-PERSONAL-API-TOKEN' \
  -H 'X-Org-Token: YOUR-V2-ORGANIZATION-TOKEN'
```

> The above command returns no data and a `204` response code when successful.

This endpoint deletes the external ticket reference.

<aside class="notice">
Remember - you can only request external ticket reference scoped to the organization specified in the
<code>X-Org-Token</code> header.
</aside>

### Ticketing System

- `azure_devops_boards`: Azure DevOps Boards
- `github`: GitHub
- `jira`: Jira
