---
weight: 15
title: Rate Limits
---

# Rate Limits

The Cobalt API sets rate limits API requests to manage request volume and maintain system availability.
Here are some details on the rate limit policy that Cobalt API implements:

- Rate limiting follows a **fixed-window policy**, with a maximum number of requests allowed in a specific
time window.
- Rate limiting applies on a **per-user basis**, regardless of how many API tokens the user has.

## Rate Limits

| Request Type    | HTTP Verbs                       | Limit | Window     | HTTP Response Headers                                    |
|-----------------|----------------------------------|-------|------------|----------------------------------------------------------|
| Get requests    | `GET`                            | 100   | 60 seconds | `X-Rate-Limit-Get-Limit` and  `X-Rate-Limit-Remaining`   |
| Mutate requests | `POST`, `PATCH`, `PUT`, `DELETE` | 20    | 60 seconds | `X-Rate-Limit-Mutate-Limit` and `X-Rate-Limit-Remaining` |

## HTTP Response Headers

- `X-Rate-Limit-Get-Limit`: Indicates the maximum number of `GET` requests allowed per time window.
Example: `X-Rate-Limit-Get-Limit: 100`
- `X-Rate-Limit-Mutate-Limit`: Indicates the maximum number of Mutate requests allowed per time window.
Example: `X-Rate-Limit-Mutate-Limit: 20`
- `X-Rate-Limit-Remaining`: Indicates the number of requests remaining in the time window
Example: `X-Rate-Limit-Remaining: 93`

## When the Rate Limit Is Exceeded

When a user exceeds the rate limit, the API returns a `509 BANDWIDTH_LIMIT_EXCEEDED` HTTP response code along with [the
headers above](#http-response-headers). The rate limit resets after the specified time window.
