---
weight: 13
title: Errors
---

# Errors

<aside class="notice">This error section helps you identify the type of error you're running into. If you think you're
experiencing a bug, or seeing incorrect data please reach out: <strong>integrations@cobalt.io</strong></aside>

The Cobalt API uses the following error codes:

| Error Code | Meaning                                                                                                    |
|------------|------------------------------------------------------------------------------------------------------------|
| 400        | Bad Request -- Your request is not good                                                                    |
| 401        | Unauthorized -- Your API token is wrong                                                                    |
| 403        | Forbidden -- You don't have access to this                                                                 |
| 404        | Not Found -- The specified request could not be found                                                      |
| 405        | Method Not Allowed -- You tried to access Cobalt data with an invalid method                               |
| 406        | Not Acceptable -- You requested a format that isn't json                                                   |
| 409        | Conflict -- You attempted to create a resource with the same `Idempotency-Key` header as a recent request. |
| 410        | Gone -- The requested endpoint has been removed from Cobalt servers                                        |
| 418        | I'm a teapot                                                                                               |
| 422        | Unprocessable Entity -- The content and syntax are correctly formed, but something else is off.            |
| 429        | Too Many Requests -- You're making requests too often! Slow down!                                          |
| 500        | Internal Server Error -- We had a problem with our server. Try again later.                                |
| 503        | Service Unavailable -- We're temporarially offline for maintanance. Please try again later.                |
