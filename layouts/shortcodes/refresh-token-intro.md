Refreshes a [personal API token](.#personal-api-token) by revoking it and creating a new token with the same name.

To refresh an API token:

1. Make a `GET` request to the `/tokens` endpoint, and save the `id` of the token that you want to refresh.
1. Make a `POST` request to the `/tokens/YOUR-TOKEN-ID/refresh` endpoint using the token `id` that you obtained.
1. From the output, save the value of the `secret` field. This is your new API token. Your old token will no longer work.

If you forgot your token, you can regenerate it in your [Cobalt profile](https://app.cobalt.io/settings/api-token). Revoke the old token, and then create a new one.