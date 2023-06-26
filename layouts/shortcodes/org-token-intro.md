Most API calls are scoped to a specific organization, with the `X-Org-Token` header. We include this header
in our API calls when needed.

To retrieve an organization token:

1. [Get all organizations](./#get-all-organizations) that you belong to.
1. From the output, save the `token` value of the desired organization.

When required, include the organization token as a header in your requests: