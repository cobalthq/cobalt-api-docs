---
weight: 16
title: Tokens
---

# Tokens

## Get All Tokens

```shell
curl -X GET "https://api.cobalt.io/tokens" 
  -H "accept: application/vnd.cobalt.v1+json" 
  -H "Authorization: Bearer your-personal-api-token-here" 

```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "resource": {
        "id": "34",
        "last_characters": "9qy7",
        "expire_at": null
      }
    }
 ]
}

```

This endpoint retrieves a list of all tokens that belong to you. 

### HTTP Request

`GET https://api.cobalt.io/tokens`

### URL Parameters

Parameter | Default | Description
--------- | ------- | -----------
limit | 100 | If set, you can adjust the limit returned, e.g. https://api.cobalt.io/tokens?limit=1000

### Fields

Field             | Description
----------------- | -----------
`id`              | Integer field used in the POST request to refresh your token
`last_characters` | Last four digits of your token for recall
`expire_at`       | null (not currently implemented)

