---
weight: 98
title: Changelog
---

# Changelog

## New Endpoints

In the v2 release, we published additional endpoints to extend the capabilities of the Cobalt API. Please refer to
the following endpoints for more details:

- **Assets**:
  - [Get an Asset](./#get-an-asset)
  - [Create an Asset](./#create-an-asset)
  - [Update an Asset](./#update-an-asset)
  - [Delete an Asset](./#delete-an-asset)
  - [Upload an Asset Attachment](./#upload-an-attachment)
  - [Delete an Asset Attachment](./#delete-an-attachment)
  - [Upload an Asset Logo](./#upload-a-logo)
- **Pentests**:
  - [Get a Pentest](./#get-a-pentest)
  - [Get a Pentest Report](./#get-a-pentest-report)
  - [Duplicate a Pentest](./#duplicate-a-pentest)
  - [Delete a Pentest](./#delete-a-pentest)
- **Findings**:
  - [Get a Finding](./#get-a-finding)
  - [View Available Finding States](./#view-available-finding-states)
  - [Update Finding State](./#update-finding-state)
- **Webhooks**:
  - [Get All Webhooks](./#get-all-webhooks)
  - [Get a Webhook](./#get-a-webhook)
  - [Create a Webhook](./#create-a-webhook)
  - [Update a Webhook](./#update-a-webhook)
  - [Delete a Webhook](./#delete-a-webhook)

## Identifier Changes

In v2, we focused on standardizing and extending identifiers for all endpoints. As a result, either
the structure or the length of some identifiers has changed. You can compare the format of identifiers for v1 and v2
in the table below.

| Endpoint                          | Response Parameter      | Example for v1         | Example for v2                                     |
|-----------------------------------|---------------------|----------------------|--------------------------------------------------|
| [organizations](./#organizations) | `id`                | or_A2bb4FE           | or_Uevoq7MyoYsPT9NPc3conL                        |
| [organizations](./#organizations) | `token`             | ABCDEFGHJ12345678901 | ASDFGHJKLQWERTYUM1234567890ABCDEFGH1234567891234 |
| [assets](./#get-all-assets)       | `id`                | as_rvZRC5Y           | as_GZgcehapJUNh6mjNuqsE4T                        |
| [assets](./#get-all-assets)       | `attachments.token` | att_yYXZodA          | at_LA5GcEL4HRitFGCHREqmzL                        |
| [pentests](./#get-all-pentests)   | `id`                | pt_rVShby8           | pt_JQJpAAMjyc8xVtXW2X2Aq5                        |
| [findings](./#findings)           | `id`                | vu_ZzZuekb           | vl_3xP2RCWWUajc3oRXmbQ4j9                        |
| [findings](./#findings)           | `pentest_id`        | pt_9Ig1234           | pt_PEtv4xqnwGV2efZhLw3XM5                        |
| [findings](./#findings)           | `asset_id`          | as_cwrsqsL           | as_HcChCMueiPQQgvckmZtRSd                        |
| [events](./#events)               | `id`                | 277603               | ac_Y35JcpGoakrjUSVjtVpXyH                        |
| [events](./#events)               | `subject.id`        | 277603               | ac_Y35JcpGoakrjUSVjtVpXyH                        |

For most endpoints, only the identifier length has changed. We also changed the prefix and type
of some identifiers. For example, the `id` prefix in the [findings](./#findings) endpoint has changed from `vu` to `vl`.
Similarly, the `attachments.token` prefix has changed from `att` to `at`.

We don't expect any of these changes to be disruptive for most of our customers. However, if you have any
validations of prefixes or string lengths in place, please update them accordingly.

The `token` attribute in the [organizations](./#organizations) endpoint returns a different string in v2.
In our API documentation, we refer to this value as the [organization token](./#organization-token).
Add the token value to the `X-Org-Token` header in your requests.

## Renamed Response Attributes

> Attribute Samples

```json
{
  // v1
  "attachments": [
    {
      "token": "att_yYXZodA"
    }
  ],

  // v2
  "attachments": [
    {
      "id": "at_LA5GcEL4HRitFGCHREqmzL"
    }
  ]
}
```

In v2, we renamed the `token` attribute of the `attachments` object in the [assets](./#get-all-assets)
endpoint to `id`.

## New Response Attributes

In v2, when you retrieve [findings](./#findings), the response contains the `attachments` attribute that
shows files attached to a finding. You can download attachments programmatically using this information.

## Request Headers

| Header          | v1                             | v2                                     | Description                                |
|-----------------|--------------------------------|----------------------------------------|--------------------------------------------|
| `Accept`          | `application/vnd.cobalt.v1+json` | `application/vnd.cobalt.v2+json`         | Required for all requests.             |
| `Content-Type`    | N/A                            | `application/vnd.cobalt.v2+json`         | Required for `POST`, `PUT`, and `DELETE` requests.  |
| `Idempotency-Key` | N/A                            | Refer to [Idempotency](./#idempotency). | Recommended for `POST` requests.                |

In v1, the Cobalt API was read-only. In v2, we added endpoints for creating, updating, and deleting resources.

To support these changes, we added the following headers:

- `Content-Type`
- `Idempotency-Key`

## Pagination Defaults

In v1, the default pagination value was 10 for some endpoints and 1000 for others. In v2, we
set the default pagination value for all endpoints to 10. This change affected the following endpoints:

| Endpoint                     | Default for v1  | Default for v2  |
|------------------------------|---------------|--------------|
| [pentests](./#pentests) | 1000          | 10           |
| [findings](./#findings) | 1000          | 10           |
