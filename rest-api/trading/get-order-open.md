---
description: This API retrieves the list of open orders on the platform.
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

# Get Open Orders

#### Prerequisites

Before using this endpoint, ensure you have read the [How to Generate a Signature](../../authentication.md) guide. This guide explains the steps required to create the `signature` parameter needed to authenticate your request.

#### Key Notes

1. The request requires specific query parameters to filter results. See details below.
2. You must provide a valid `timestamp` and `signature` in the query parameters.
3. The `x-api-key` must be included in the request headers for authentication.

## Get Open Orders

<mark style="color:green;">`GET`</mark> `https://nami.exchange/api/v4/spot/open`

**Headers**

| Name         | Value               |
| ------------ | ------------------- |
| Content-Type | `application/json`  |
| x-api-key    | `<Your secret key>` |

**Query Parameters**

| Name            | Type      | Description                                              | Required | Example   |
| --------------- | --------- | -------------------------------------------------------- | -------- | --------- |
| `filterByPair`  | string    | Filter open orders by a specific trading pair (e.g., BTC/USD). | No       | BTC/USD   |
| `signature`     | string    | The signature is the secret key encoded as ASCII data. It is required for authenticating the request. | Yes      | a1b2c3d4e5f6g7h8i9j0k |
| `timestamp`     | date-time | The timestamp is the time the request was sent.          | Yes      | 1670000000000 |

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
  "status": "ok",
  "data": [
    {
      "price": 35000,
      "stopPrice": null,
      "quantity": 1.2,
      "executedQty": 0.6,
      "quoteQty": 42000,
      "executedQuoteQty": 21000,
      "useQuoteQty": false,
      "liquidityStatus": 1,
      "liquiditySymbol": "BTC/USD",
      "liquidityUsdtPrice": 1,
      "liquidityTransferPrice": 35000,
      "liquidityOrderId": "12537485",
      "displayingId": 453672,
      "userId": 25,
      "side": "BUY",
      "type": "LIMIT",
      "symbol": "BTC/USD",
      "baseAsset": "BTC",
      "baseAssetId": 1,
      "quoteAsset": "USD",
      "quoteAssetId": 22,
      "status": "NEW",
      "createdAt": "2025-01-10T14:25:33.524Z",
      "updatedAt": "2025-01-12T16:40:11.124Z"
    }
  ]
}
```

{% endtab %}

{% tab title="400" %}
```json
{
    "status": "BROKER_ERROR",
    "code": 6104,
    "data": {
        "requestId": "6ff66697-2742-4caf-acad-f97e9cc3596d"
    },
    "message": null
}
```
{% endtab %} {% endtabs %}