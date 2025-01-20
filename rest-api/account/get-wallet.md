---
description: This API retrieves the balance details of a user's wallet for a specific currency.
layout:
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Get User Wallet Balance

#### Prerequisites

Before using this endpoint, ensure you have read the [How to Generate a Signature](../../authentication.md) guide. This guide explains the steps required to create the `signature` parameter needed to authenticate your request.

#### Key Notes

1. The request requires a valid `timestamp` and `signature` in the query parameters.
2. The `x-api-key` must be included in the request headers for authentication.

## Get User Wallet Balance

<mark style="color:green;">`GET`</mark> `https://nami.exchange/api/v4/user/balance`

**Headers**

| Name         | Value               |
| ------------ | ------------------- |
| Content-Type | `application/json`  |
| x-api-key    | `<Your secret key>` |

**Query Parameters**

| Name        | In    | Type     | Description                          | Required | Example |
| ----------- | ----- | -------- | ------------------------------------ | -------- | ------- |
| `currency`  | query | integer  | The currency symbol (ID).            | No       | 1       |
| `signature`     | query | string    | The signature is the secret key encoded as ASCII data. It is required for authenticating the request. | Yes      | a1b2c3d4e5f6g7h8i9j0k |
| `timestamp`     | query | date-time | The timestamp is the time the request was sent.          | Yes      | 1670000000000 |

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
  "status": "ok",
  "data": {
    "1": {
      "value": 0,
      "locked_value": 0,
      "type": 0
    },
    "2": {
      "value": 0,
      "locked_value": 0,
      "type": 0
    }
  }
}
```
{% endtab %}

{% tab title="400" %}
```json
{
    "statusCode": 401,
    "message": "Missing API key, signature, or timestamp",
    "error": "Unauthorized"
}
```
{% endtab %} {% endtabs %}