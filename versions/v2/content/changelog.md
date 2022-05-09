---
weight: 98
title: Changelog
---

# Changelog

## New Endpoints

In the v2 release, we've published some additional endpoints to extend the capabilities of Cobalt API. Please refer to
the following endpoints for more details:

- [Get an Asset](#get-an-asset)
- [Delete an Asset](#delete-an-asset)
- [Get a Pentest](#get-a-pentest)
- [Get a Finding](#get-a-finding)
- [View Available Finding States](#view-available-finding-states)
- [Update Finding State](#update-finding-state)

## Identifier Changes

In Cobalt API v2, we've focused on standardizing and extending identifiers for all endpoints. As a result, either
the structure or the length of some identifiers has changed. You can see a side-by-side comparison of v1 and v2
with some sample identifiers below:

| Endpoint                        | Response field      | v1 (example)         | v2 (example)                           |
|---------------------------------|---------------------|----------------------|--------------------------------------------------|
| [organizations](#organizations) | `id`                | or_A2bb4FE           | or_Uevoq7MyoYsPT9NPc3conL                        |
| [organizations](#organizations) | `token`             | ABCDEFGHJ12345678901 | ASDFGHJKLQWERTYUM1234567890ABCDEFGH1234567891234 |
| [assets](#get-all-assets)       | `id`                | as_rvZRC5Y           | as_GZgcehapJUNh6mjNuqsE4T                        |
| [assets](#get-all-assets)       | `attachments.token` | att_yYXZodA          | at_LA5GcEL4HRitFGCHREqmzL                        |
| [pentests](#get-all-pentests)   | `id`                | pt_rVShby8           | pt_JQJpAAMjyc8sVtXW2X2Aq5                        |
| [findings](#findings)           | `id`                | vu_ZzZuekb           | vl_3sP2RCWWUajc3oRXmbQ4j9                        |
| [findings](#findings)           | `pentest_id`        | pt_9Ig1234           | pt_PEtv4dqnwGV2efZhLw3BM5                        |
| [findings](#findings)           | `asset_id`          | as_cwrsqsL           | as_HcChCMueiPQQgvckmZtRSd                        |
| [events](#events)               | `id`                | 277603               | ac_Y35JcpGoakrjUSVjtVpXyH                        |
| [events](#events)               | `subject.id`        | 277603               | ac_Y35JcpGoakrjUSVjtVpXyH                        |

For the majority of endpoints, the only change is the length of the identifier. However, there are some prefix and type
changes too. For example, the identifier prefix of the findings endpoint has changed from `vu` to `vl`. Similarly,
the `attachments.token` prefix has changed from `att` to `at`.

We aren't expecting any of these to be breaking changes for the majority of our customers, but, if you have any
validations in place, concerning prefixes or the length of strings, please update them accordingly.

Please note - the `token` attribute of the [organizations](#organizations) endpoint now returns a different string in
v2. This value is also known as "organization token" all over the API docs, and is used as the value of `X-Org-Token`
header when calling endpoints.

## Renamed Response Attributes

The `token` attribute of the `attachments` object in `v1` of [assets](#get-all-assets) endpoint was renamed to `id` in `v2`.

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

## Request Headers

| Header          | v1                             | v2                                   | Description                                |
|-----------------|--------------------------------|--------------------------------------|--------------------------------------------|
| Accept          | application/vnd.cobalt.v1+json | application/vnd.cobalt.v2+json       | Must be present in the request             |
| Content-Type    | N/A                            | application/vnd.cobalt.v2+json       | Required for POST/PUT/DELETE HTTP methods  |
| Idempotency-Key | N/A                            | Refer to [idempotency](#idempotency) | Suggested for POST requests |

In v1, the Cobalt API was read-only, and in v2 we've added different endpoints where you can create, update or delete
resources.

With these additions in place, two new headers came into place; `Content-Type` and `Idempotency-Key`. The
`Idempotency-Key` is explained in the [idempotency](#idempotency) section.

## Pagination Defaults

In v1, some endpoints had 10, and some others had 1000 as their pagination default value. In this release, we've
updated the default pagination values of all endpoints to 10. Two endpoints were affected by this change:

| Endpoint                        | v1 (default)  | v2 (default) |
|---------------------------------|---------------|--------------|
| [pentests](#organizations)      | 1000          | 10           |
| [findings](#organizations)      | 1000          | 10           |
