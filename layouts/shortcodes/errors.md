<aside class="notice">
If you think you've encountered a bug, or you see incorrect data, please contact us:
<a href="mailto:" target="_blank">integrations@cobalt.io</a>.
</aside>

The Cobalt API uses the following HTTP response status codes for errors:

| HTTP Response Status Code | Meaning                                                                                                |
|------------|--------------------------------------------------------------------------------------------------------|
| 400 Bad Request       | The server can't process your request due to a client error.                                |
| 401 Unauthorized      | Your API token is wrong.                                                                    |
| 403 Forbidden       | You don't have access to this resource.                                                       |
| 404 Not Found       | The specified request couldn't be found.                                                      |
| 405 Method Not Allowed       | You tried to access Cobalt data using an invalid method.                             |
| 406 Not Acceptable       | You requested a format that isn't JSON.                                                  |
| 409 Conflict | You attempted to create a resource with the same `Idempotency-Key` header as in your recent request. |
| 410 Gone       | The requested endpoint has been removed from Cobalt servers.                                       |
| 418 I'm a teapot       | The server refuses to process this request.                                                |
| 422 Unprocessable Content | The content and syntax are formed properly, but something else is off.                  |
| 429 Too Many Requests       | You're making requests too often.                                                     |
| 500 Internal Server Error       | We had a problem with our server. Try again later.                                |
| 503 Service Unavailable       | We're temporarily offline for maintenance. Please try again later.                  |