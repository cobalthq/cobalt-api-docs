---
weight: 13
title: Pagination
---

# Pagination

Pagination can be used if the number of resources for a request exceeds the value of the `limit` query parameter of the
request. If the `next_page` and/or `prev_page` values in the response are non-`null` there are additional resources.
To paginate append the `next_page` or `prev_page` value to the base API URL.

For example, if the `next_page` value in a response is `/resource?cursor=a1b2c3d4` you can send the following request
for the next page.

`GET https://api.cobalt.io/resource?cursor=a1b2c3d4`

<aside class="success">
Remember — there is always a default value for the <code>limit</code> query parameter.
</aside>
