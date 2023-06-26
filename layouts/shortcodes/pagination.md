When the number of resources in the response exceeds the value of the `limit` query parameter, you can use pagination.
If the `next_page` and/or `prev_page` values in the response are not `null`, it means that the response contains
additional resources. To paginate the response, append the `next_page` or `prev_page` value to the base API URL.

For example, if the `next_page` value in the response is `/resource?cursor=a1b2c3d4`, send the following request for the next page:

`GET https://api.cobalt.io/resource?cursor=a1b2c3d4`