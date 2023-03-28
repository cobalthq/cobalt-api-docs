---
weight: 15
title: Rate Limits
---

# Rate Limits

Cobalt API provides rate limiting on API requests to manage request volume and provide a reliable and available API.
Here are some details on the rate limit policy that Cobalt API implements:

- Rate limiting follows a **Fixed-Window policy** where there is a maximum amount of requests allowed in a specific
window of time.
- Rate limiting is applied on a **per-user basis**, regardless of how many API tokens the user owns.

## Rate Limits

| Request Type    | HTTP Verb                     | Limit | Window     | HTTP Response Headers                                   |
|-----------------|-------------------------------|-------|------------|---------------------------------------------------------|
| Get Requests    | `GET`                         | 100   | 60 seconds | `X-Rate-Limit-Get-Limit` and  `X-Rate-Limit-Remaining`  |
| Mutate Requests | `POST` `PATCH` `PUT` `DELETE` | 20    | 60 seconds | `X-Rate-Limit-Mutate-Limit`and `X-Rate-Limit-Remaining` |

## HTTP Response Headers

- `X-Rate-Limit-Get-Limit`: indicates the maximum rate allowed for `GET` requests.
Example: `X-Rate-Limit-Get-Limit: 100`
- `X-Rate-Limit-Mutate-Limit`: indicates the maximum rate allowed for Mutate requests.
Example: `X-Rate-Limit-Mutate-Limit: 20`
- `X-Rate-Limit-Remaining`: indicates the number of requests left in the window of time.
Example: `X-Rate-Limit-Remaining: 93`

## When Rate Limit is Exceeded

When a user exceeds the rate limit, the API will return HTTP `509 BANDWIDTH_LIMIT_EXCEEDED` response code and message
along with the headers above. The user will have to wait no more than the window of time above in order for the
rate limit to reset.
