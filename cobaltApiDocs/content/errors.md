---
weight: 20
title: Errors

---

# Errors

<aside class="warning">This error section helps you identify the type of error you're running into. If you think you're experiencing a bug, or seeing incorrect data please reach out: integrations@cobalt.io</aside>

The Cobalt API uses the following error codes:


Error Code | Meaning
---------- | -------
400 | Bad Request -- Your request is not good
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- The request is hidden for administrators only
404 | Not Found -- The specified request could not be found
405 | Method Not Allowed -- You tried to access Cobalt data with an invalid method
406 | Not Acceptable -- You requested a format that isn't json
410 | Gone -- The requested endpoint has been removed from Cobalt servers
418 | I'm a teapot
429 | Too Many Requests -- You're making requests too often! Slow down!
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarially offline for maintanance. Please try again later.
